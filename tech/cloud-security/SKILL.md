---
name: cloud-security
description: >
  Expert sécurité cloud et infrastructure pour HB Digital. Déclenche sur :
  sécurité serveur, VPS, HTTPS, SSL, certificat, pare-feu, firewall, accès SSH,
  sécurité WordPress, vulnérabilité, RGPD infrastructure, sécurité base de données,
  backup, sauvegarde, mot de passe serveur, protection DDoS, sécurité API,
  variables d'environnement, données personnelles hébergement, audit sécurité.
  Stack HB Digital : VPS OVH/Hetzner, WordPress, PHP, Python, Nginx/Apache,
  MySQL, Amazon SES, scripts Python hébergés. Self-healing : donne des
  recommandations actionnables même sans accès à l'infrastructure.
---

# Cloud Security — HB Digital Performance

## Contexte infrastructure HB Digital

| Composant | Technologie | Risques principaux |
|---|---|---|
| VPS / Serveurs | OVH, Hetzner (~5€/mois) | Accès SSH non sécurisé, root ouvert |
| Sites WordPress | PHP + MySQL | Plugins obsolètes, injections SQL |
| Scripts Python | Cron jobs | Credentials en dur, logs exposés |
| Tracker affilié maison | Node.js / Python + SQLite/PostgreSQL | Accès base de données, fuite leads |
| Emails | Amazon SES, Brevo | SPF/DKIM/DMARC, réputation IP |
| Landing pages | HTML statique / WordPress | Formulaires non protégés |
| Données leads | CSV, BDD | RGPD, fuite, accès non autorisé |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Pas d'accès au serveur | Donner les commandes à copier-coller |
| OS non précisé | Ubuntu 22.04 LTS par défaut |
| Panel non précisé | Recommander configuration manuelle SSH |
| Audit sans accès | Checklist + questions de diagnostic |

---

## ÉTAPE 1 — Hardening VPS (priorité haute)

### 1.1 Sécurisation SSH (obligatoire dès le premier déploiement)

```bash
# 1. Créer un utilisateur non-root
adduser hbdigital
usermod -aG sudo hbdigital

# 2. Configurer SSH key authentication
# Sur votre machine locale :
ssh-keygen -t ed25519 -C "hbdigital@server"
ssh-copy-id hbdigital@[IP_SERVEUR]

# 3. Désactiver le login root et le password auth
nano /etc/ssh/sshd_config
# Modifier :
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
Port 2222  # changer le port par défaut (22)

# Redémarrer SSH
systemctl restart sshd
```

### 1.2 Pare-feu UFW

```bash
# Installer et configurer UFW
apt install ufw

# Règles de base
ufw default deny incoming
ufw default allow outgoing

# Autoriser uniquement ce qui est nécessaire
ufw allow 2222/tcp    # SSH (port modifié)
ufw allow 80/tcp      # HTTP
ufw allow 443/tcp     # HTTPS

# Activer
ufw enable
ufw status
```

### 1.3 Fail2ban (protection brute force)

```bash
apt install fail2ban

# Configuration
cat > /etc/fail2ban/jail.local << 'EOF'
[DEFAULT]
bantime = 3600
findtime = 600
maxretry = 5

[sshd]
enabled = true
port = 2222
logpath = %(sshd_log)s

[nginx-http-auth]
enabled = true
EOF

systemctl restart fail2ban
```

---

## ÉTAPE 2 — Sécurité HTTPS / SSL

### 2.1 Let's Encrypt avec Certbot (gratuit)

```bash
# Installer Certbot
apt install certbot python3-certbot-nginx

# Obtenir le certificat
certbot --nginx -d example.com -d www.example.com

# Renouvellement automatique (déjà configuré via cron)
certbot renew --dry-run

# Vérifier la configuration SSL
curl -sI https://example.com | grep -i "Strict-Transport"
```

### 2.2 Headers de sécurité HTTP (Nginx)

```nginx
# Dans /etc/nginx/sites-available/votre-site
server {
    # ...
    
    # Headers de sécurité
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "strict-origin-when-cross-origin" always;
    add_header Content-Security-Policy "default-src 'self' https:; script-src 'self' https: 'unsafe-inline'; style-src 'self' https: 'unsafe-inline'" always;
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    
    # Masquer la version Nginx
    server_tokens off;
}
```

---

## ÉTAPE 3 — Sécurité WordPress

### 3.1 Checklist WordPress sécurité

```bash
# 1. Table prefix personnalisé (lors de l'installation)
# Ne pas utiliser "wp_" par défaut

# 2. Fichier wp-config.php — permissions restrictives
chmod 600 wp-config.php
chown www-data:www-data wp-config.php

# 3. Désactiver l'édition de fichiers depuis l'admin
# Dans wp-config.php :
define('DISALLOW_FILE_EDIT', true);

# 4. Désactiver l'affichage des erreurs PHP en production
define('WP_DEBUG', false);
define('WP_DEBUG_DISPLAY', false);
```

**Via Nginx — Protéger wp-admin :**
```nginx
# Restreindre wp-admin par IP
location /wp-admin {
    allow [VOTRE_IP];
    deny all;
}

# Bloquer xmlrpc.php (vecteur d'attaque DDoS)
location = /xmlrpc.php {
    deny all;
}
```

### 3.2 Plugins de sécurité recommandés

| Plugin | Usage | Coût |
|---|---|---|
| **Wordfence** | Firewall WAF + scan malware | Gratuit (limité) / 99$/an |
| **WP Hide Login** | Changer l'URL de /wp-login.php | Gratuit |
| **Limit Login Attempts** | Blocage brute force login | Gratuit |
| **UpdraftPlus** | Sauvegardes automatiques | Gratuit (basique) |

---

## ÉTAPE 4 — Protection des données (RGPD)

### 4.1 Obligations RGPD pour HB Digital

```
DONNÉES LEADS (formulaires) :
→ Consentement explicite recueilli et horodaté
→ Durée de conservation limitée (3 ans max recommandé)
→ Droit d'accès et de suppression opérationnel
→ Registre des traitements tenu à jour

HÉBERGEMENT :
→ Préférer hébergement EU (OVH, Scaleway, Hetzner UE)
→ Pas de transfert vers pays hors EU sans garanties
→ Amazon SES : serverless US → acceptable si DPA signé

SOUS-TRAITANTS :
→ DPA signé avec chaque sous-traitant (Brevo ✅, Meta ✅, Google ✅)
```

### 4.2 Sécurisation de la base de données leads

```bash
# MySQL — Sécurisation de base
# Créer un utilisateur dédié (pas root)
CREATE USER 'hbdigital_app'@'localhost' IDENTIFIED BY '[MOT_DE_PASSE_FORT]';
GRANT SELECT, INSERT, UPDATE ON leads_db.* TO 'hbdigital_app'@'localhost';
FLUSH PRIVILEGES;

# Ne jamais se connecter en root depuis l'application

# Chiffrement des données sensibles (emails, téléphones)
# Utiliser AES_ENCRYPT() en MySQL ou chiffrement applicatif en Python
```

---

## ÉTAPE 5 — Sécurité email (délivrabilité et anti-spam)

### 5.1 Configuration DNS obligatoire

```
SPF (TXT sur le domaine) :
v=spf1 include:_spf.brevo.com include:amazonses.com ~all

DKIM :
Généré par Brevo/SES, à ajouter en TXT dans le DNS

DMARC :
_dmarc.votredomaine.com TXT "v=DMARC1; p=quarantine; rua=mailto:dmarc@votredomaine.com"

Vérification :
mail-tester.com → tester le score de délivrabilité
mxtoolbox.com → vérifier SPF/DKIM/DMARC
```

### 5.2 Checklist délivrabilité pré-envoi

- [ ] SPF configuré et valide ?
- [ ] DKIM configuré et signé ?
- [ ] DMARC configuré ?
- [ ] Reverse DNS configuré sur l'IP d'envoi ?
- [ ] Score mail-tester.com > 9/10 ?
- [ ] Liste nettoyée (supprimer les bounces durs) ?
- [ ] Taux désabonnement < 0.5% ?

---

## ÉTAPE 6 — Backup et continuité

### 6.1 Stratégie de backup 3-2-1

```
RÈGLE 3-2-1 :
→ 3 copies des données
→ sur 2 supports différents
→ dont 1 hors site (cloud)

Pour HB Digital :
- Backup quotidien VPS → objet storage (OVH Cold, Backblaze B2)
- Backup WordPress quotidien via UpdraftPlus → Google Drive
- Backup BDD leads → export quotidien chiffré + envoi email

Script backup MySQL automatique :
```

```bash
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backup/mysql"
DB_NAME="leads_db"

mysqldump -u root -p[PASS] $DB_NAME | gzip > $BACKUP_DIR/${DB_NAME}_${DATE}.sql.gz

# Supprimer les backups > 30 jours
find $BACKUP_DIR -name "*.sql.gz" -mtime +30 -delete

# Envoyer vers S3 / objet storage
aws s3 cp $BACKUP_DIR/${DB_NAME}_${DATE}.sql.gz s3://[BUCKET]/mysql/
```

---

## FORMAT DE SORTIE

```
## Audit Sécurité — [Composant]

**Composants analysés :** [liste]

**Niveau de risque global :** [🔴 Élevé / 🟡 Moyen / 🟢 Faible]

**Problèmes critiques :**
🔴 [Problème 1] — [Risque concret] — [Correction immédiate]
🔴 [Problème 2] — ...

**Améliorations importantes :**
🟡 [Amélioration 1] — [Commandes / config]

**Checklist de conformité RGPD :**
□ [Point 1] — [statut]
□ [Point 2] — [statut]

**Plan d'action :**
| Priorité | Action | Délai | Complexité |
|---|---|---|---|
| 1 | [action] | Aujourd'hui | Faible |
| 2 | [action] | Cette semaine | Moyenne |

**Prochaine étape :** [action précise à faire dans les 2h]
```

---

## RÈGLES ABSOLUES

1. Sécuriser SSH en priorité absolue sur tout nouveau VPS (avant toute autre config)
2. Jamais de credentials en dur dans le code ou les scripts
3. HTTPS obligatoire en production — Let's Encrypt est gratuit, zéro excuse
4. Backup quotidien + test de restauration mensuel
5. Finir par les actions critiques à faire immédiatement, dans l'ordre
