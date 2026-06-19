---
name: churn-prevention
description: >
  Expert rétention et prévention du churn pour HB Digital. Déclenche sur :
  client qui part, résilier, perte de client, retention, fidélisation, réduire
  le churn, client inactif, renouvellement contrat, upsell, client à risque,
  NPS, satisfaction client, win-back, campagne réengagement, reconquête client
  perdu. Couvre : clients annonceurs, affiliés partenaires, clients PME
  consulting, abonnés SEYDI Paris. Self-healing : produit un plan de rétention
  même sans données de churn disponibles.
---

# Churn Prevention — HB Digital Performance

## Contexte rétention HB Digital

| Segment | Churn principal | Valeur client | Priorité rétention |
|---|---|---|---|
| Annonceurs leads | Fin de budget / résultats décevants | 500-5 000 €/mois | Très haute |
| Affiliés partenaires | Offres concurrentes meilleures | 100-2 000 €/mois | Haute |
| Clients consulting | Insatisfaction ROI / recrutement interne | 800-3 500 €/mois | Très haute |
| Abonnés SEYDI Paris | Non-réachat / désabonnement email | 60-300 € LTV | Moyenne |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Pas de données churn | Utiliser les benchmarks sectoriels + créer un système de mesure |
| Churn non défini | Proposer la définition standard adaptée |
| Pas d'historique client | Travailler sur les signaux comportementaux disponibles |
| Segment non précisé | Couvrir les 4 segments HB Digital |

---

## ÉTAPE 1 — Mesure et diagnostic du churn

### 1.1 Définitions par segment

```
ANNONCEURS / CLIENTS CONSULTING :
Churn = résiliation du contrat ou fin de collaboration
Churn mensuel = (clients perdus / clients en début de mois) × 100
Cible : < 5%/mois (soit > 20 mois de vie client en moyenne)

AFFILIÉS :
Churn = inactif > 60 jours (pas de leads/clics générés)
Cible : < 10% d'affiliés inactifs par trimestre

SEYDI PARIS :
Churn = pas de commande depuis > 12 mois
Email churn = désabonnement newsletter
Cible e-com : taux de réachat > 30% à 12 mois
```

### 1.2 Calcul LTV (Life Time Value)

```
LTV = Panier moyen × Fréquence d'achat × Durée relation (mois)

Exemple Annonceur consulting :
  Panier moyen = 1 500 €/mois
  Durée moyenne = 8 mois
  LTV = 1 500 × 8 = 12 000 €

Exemple SEYDI :
  Panier moyen = 95 €
  Fréquence = 1.8 commandes/an
  Durée = 2.5 ans
  LTV = 95 × 1.8 × 2.5 = 427 €

→ Justification du budget de rétention = LTV × taux de sauvegarde estimé
```

### 1.3 Signaux d'alerte (leading indicators)

**Annonceurs / clients consulting :**
- Diminution des contacts (moins de messages, appels, réunions)
- Questions sur le contrat ou la période de préavis
- Réductions de budget demandées
- Comparaison active avec des alternatives
- Délais de paiement qui s'allongent

**Affiliés :**
- Volume de leads/clics en baisse > 30% vs M-1
- Non-lecture des communications
- Ticket de support ouvert sans résolution rapide
- Demande de changement des conditions

**E-commerce (SEYDI) :**
- Dernier achat > 6 mois
- Désabonnement de la newsletter
- Abandon de panier répété sans achat
- Retours produit

---

## ÉTAPE 2 — Stratégie de prévention

### 2.1 Segmentation clients par risque

```
MATRICE DE RISQUE :

Score risque = f(ancienneté, CA, engagement, signaux d'alerte)

🔴 RISQUE ÉLEVÉ — Action immédiate
├── Critères : signal d'alerte présent + CA important
├── Action : appel direct dans les 48h
└── Budget : jusqu'à 20% du CA mensuel en geste commercial

🟡 RISQUE MOYEN — Surveillance active
├── Critères : engagement en baisse mais pas d'alerte
├── Action : email personnalisé + rapport de valeur
└── Budget : jusqu'à 10% du CA mensuel

🟢 RISQUE FAIBLE — Nurturing standard
├── Critères : client satisfait, engagement normal
├── Action : communication régulière + upsell
└── Budget : < 5% du CA mensuel
```

### 2.2 Plan de rétention par segment

**Annonceurs / Clients consulting :**

```
J0 — Onboarding (prévention dès le début)
→ QBR (Quarterly Business Review) planifié dès le contrat
→ Rapport de valeur mensuel automatique
→ Point de satisfaction à J+30 et J+90

M3 — First Value Check
→ Bilan des résultats vs objectifs fixés
→ Ajustement si nécessaire
→ Proposition d'optimisation ou d'upsell

Signal d'alerte détecté :
→ Appel dans les 48h (pas d'email — appel)
→ Agenda partagé pour un bilan express
→ Proposition de plan d'action concret

Risque élevé confirmé :
→ Geste commercial : mois offert / audit gratuit / bonus leads
→ Escalade si nécessaire (Hady directement)
→ Si départ inévitable : exit interview pour apprendre
```

**Affiliés :**

```
Affilié inactif > 30 jours :
→ Email automatique : "On a remarqué que..."
→ Rappel des meilleures offres actives
→ Proposition d'un appel pour optimiser

Affilié inactif > 60 jours :
→ Email de réactivation avec incentive (commission boostée 30 jours)
→ Proposition de nouvelles verticales

Affilié inactif > 90 jours :
→ Email de clôture + invitation à revenir
→ Archivage du compte si pas de réponse
```

**SEYDI Paris (e-commerce) :**

```
30 jours sans achat :
→ Email "On vous a manqué ?" + produits recommandés basés sur l'historique

90 jours sans achat :
→ Email "Offre spéciale pour vous retrouver" + code promo (-10%)

6 mois sans achat :
→ Email win-back avec nouvelle collection + message fort sur les valeurs
→ Code promo expirant sous 7 jours (-15%)

12 mois sans achat :
→ Dernière tentative : "Voici ce que vous avez manqué"
→ Ou nettoyer la liste (meilleure délivrabilité)
```

---

## ÉTAPE 3 — Gestion du churn actif

### 3.1 Client qui annonce son départ

**Protocole en 5 étapes :**

```
ÉTAPE 1 — Écouter (pas défendre)
→ Comprendre la raison réelle (pas la raison annoncée)
→ Questions : "Qu'est-ce qui aurait pu vous faire rester ?"

ÉTAPE 2 — Reconnaître (pas excuser)
→ Valider l'insatisfaction si fondée
→ Ne pas minimiser ni promettre l'impossible

ÉTAPE 3 — Proposer (concret et rapide)
→ Action corrective immédiate si problème réparable
→ Geste commercial si insatisfaction validée
→ Alternative (contrat réduit, pause plutôt que rupture)

ÉTAPE 4 — Confirmer ou laisser partir
→ Si le client reste : mettre en place l'action + suivi J+30
→ Si le client part : exit interview + offre de retour dans 3 mois

ÉTAPE 5 — Documenter et apprendre
→ Raison du churn dans le CRM
→ Analyser si pattern récurrent
→ Ajuster le produit/service si nécessaire
```

### 3.2 Gestes commerciaux autorisés

| Situation | Geste autorisé | Limite |
|---|---|---|
| Insatisfaction résultats | Mois offert ou audit gratuit | 1 fois par client |
| Problème technique | Crédit sur prochaine facture | Valeur du préjudice |
| Concurrent moins cher | Remise ponctuelle -15% max | Sur 3 mois |
| Réduction budget client | Pack réduit (scope allégé) | Si marge reste > 25% |

---

## ÉTAPE 4 — Campagnes de win-back

### 4.1 Séquence email win-back (clients perdus)

```
Email 1 — J+30 après la fin :
Objet : "Un point sur notre collaboration"
Contenu : Récap de la valeur créée ensemble + ce qui a changé chez HB Digital
CTA : Prendre 15 minutes pour discuter

Email 2 — J+60 :
Objet : "Nouvelle offre — vous y aviez pensé ?"
Contenu : Offre révisée ou nouvelle option qui répond au problème identifié
CTA : Voir la proposition

Email 3 — J+90 (dernier) :
Objet : "On vous laisse tranquille (ou presque)"
Contenu : Succès récent + invitation ouverte à revenir
CTA : Nous contacter quand le moment sera venu
```

---

## FORMAT DE SORTIE

```
## Plan de Rétention — [Segment / Client]

**Situation :** [description du risque identifié]
**Valeur client :** XX €/mois — LTV estimée : XX €

**Score de risque :** [🔴 Élevé / 🟡 Moyen / 🟢 Faible]
**Raison probable :** [analyse]

**Actions recommandées :**
| Priorité | Action | Délai | Responsable | Budget max |
|---|---|---|---|---|
| 1 | [action] | Aujourd'hui | Hady | XX € |
| 2 | [action] | Cette semaine | | |

**Message à envoyer :**
[Draft email/message si applicable]

**KPI de suivi :**
- Taux de rétention mensuel : objectif X%
- Délai moyen détection signal : < X jours
- Taux de win-back : > X%

**Prochaine étape :** [1 action précise dans les 24h]
```

---

## RÈGLES ABSOLUES

1. Détecter les signaux d'alerte AVANT que le client annonce son départ
2. Appeler > envoyer un email pour les clients à risque élevé
3. Ne jamais promettre ce qu'on ne peut pas tenir pour retenir un client
4. Documenter chaque churn dans le CRM — les patterns sont le meilleur signal
5. Finir par 1 action concrète dans les 24h
