---
name: email-template-builder
description: >
  Constructeur de templates HTML email pour campagnes B2C et B2B chez HB Digital.
  Déclenche sur : template email, kit HTML email, design email, maquette email,
  email HTML, routing email, gabarit email, mise en page email, email responsive,
  email campagne, email transactionnel, header email, footer email, intégration ESP.
  Couvre : campagnes clients assurance/énergie/défiscalisation, newsletters HB Digital,
  SEYDI Paris, kits email pour affiliés. Self-healing : génère un template
  fonctionnel même sans spécifications complètes.
---

# Email Template Builder — HB Digital Performance

## Contexte

HB Digital produit des emails HTML pour :

| Usage | Contexte | Spécificités |
|---|---|---|
| **Campagnes clients CPL** | Assurance, énergie, défiscalisation | Volume élevé, délivrabilité critique, CTA direct |
| **Kits affiliés** | Templates pour éditeurs partenaires | Variables dynamiques, compatibilité multi-ESP |
| **Newsletter HB Digital** | B2B — annonceurs, partenaires | Branding agence, contenu éditorial |
| **SEYDI Paris** | E-commerce mode | Visuels forts, bouton achat |
| **Emails transactionnels** | Confirmation, onboarding | Fiabilité, clarté |

**ESPs compatibles cibles :** Brevo (Sendinblue), Mailjet, Amazon SES, Klaviyo, Mailchimp.

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Type email non précisé | Demander "campagne ou transactionnel ?" et démarrer |
| Branding non fourni | Utiliser couleurs neutres avec slots `[COULEUR_PRIMAIRE]` |
| Contenu non fourni | Générer avec placeholders explicites |
| ESP non précisé | Coder pour compatibilité universelle (tables + inline CSS) |
| Taille non précisée | 600px de large (standard email) |

---

## ÉTAPE 1 — Contraintes techniques email HTML

### 1.1 Règles fondamentales (non négociables)

```
STRUCTURE :
- Largeur max : 600px (desktop) / 100% (mobile)
- Mise en page : TABLES uniquement (pas de divs pour la structure)
- Images : alt text obligatoire (affichage images désactivées)
- Liens : href absolus uniquement (jamais de relative URLs)
- Caractères : UTF-8

CSS :
- Tout en INLINE (style="...") — pas de <style> externe sauf exceptions
- Pas de CSS3 avancé (ni Grid, ni Flexbox dans les tables)
- Background-image : éviter (non supporté Outlook)
- Fonts : Arial, Helvetica, Georgia, Times, Verdana (system fonts)

IMAGES :
- Format : JPG ou PNG, poids < 200ko par image
- Hébergement : URL absolue (CDN ou serveur)
- Alt text : toujours renseigné

COMPATIBILITÉ :
- Tester sur : Outlook 2016/2019/365, Gmail, Apple Mail, mobile iOS/Android
```

### 1.2 Structure HTML de base

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>[TITRE EMAIL]</title>
  <style>
    /* UNIQUEMENT pour les media queries mobile */
    @media only screen and (max-width: 600px) {
      .container { width: 100% !important; }
      .col-half { width: 100% !important; display: block !important; }
      .hide-mobile { display: none !important; }
    }
  </style>
</head>
<body style="margin: 0; padding: 0; background-color: #f4f4f4;">
  <!-- WRAPPER -->
  <table width="100%" border="0" cellpadding="0" cellspacing="0"
         style="background-color: #f4f4f4;">
    <tr>
      <td align="center" style="padding: 20px 0;">

        <!-- CONTAINER 600px -->
        <table class="container" width="600" border="0" cellpadding="0" cellspacing="0"
               style="background-color: #ffffff; border-radius: 4px;">

          <!-- HEADER -->
          <tr>
            <td style="padding: 20px 30px; background-color: [COULEUR_PRIMAIRE];">
              <img src="[LOGO_URL]" alt="[NOM_MARQUE]" width="150" style="display: block;">
            </td>
          </tr>

          <!-- HERO / BANNIÈRE -->
          <tr>
            <td>
              <img src="[HERO_IMAGE_URL]" alt="[ALT_HERO]" width="600"
                   style="display: block; max-width: 100%;">
            </td>
          </tr>

          <!-- CORPS PRINCIPAL -->
          <tr>
            <td style="padding: 30px 30px 20px 30px;">
              <h1 style="margin: 0 0 15px 0; font-family: Arial, sans-serif;
                         font-size: 24px; font-weight: bold; color: #222222;">
                [TITRE_PRINCIPAL]
              </h1>
              <p style="margin: 0 0 15px 0; font-family: Arial, sans-serif;
                        font-size: 16px; line-height: 1.6; color: #555555;">
                [CORPS_TEXTE]
              </p>

              <!-- CTA BOUTON -->
              <table border="0" cellpadding="0" cellspacing="0" style="margin: 25px 0;">
                <tr>
                  <td align="center" bgcolor="[COULEUR_CTA]" style="border-radius: 4px;">
                    <a href="[URL_CTA]" target="_blank"
                       style="display: inline-block; padding: 14px 30px;
                              font-family: Arial, sans-serif; font-size: 16px;
                              font-weight: bold; color: #ffffff; text-decoration: none;
                              border-radius: 4px;">
                      [TEXTE_CTA]
                    </a>
                  </td>
                </tr>
              </table>
            </td>
          </tr>

          <!-- FOOTER -->
          <tr>
            <td style="padding: 20px 30px; background-color: #f8f8f8;
                       border-top: 1px solid #eeeeee;">
              <p style="margin: 0; font-family: Arial, sans-serif; font-size: 12px;
                        color: #999999; text-align: center; line-height: 1.5;">
                [NOM_SOCIETE] — [ADRESSE]<br>
                <a href="[LIEN_DESABONNEMENT]" style="color: #999999;">
                  Se désabonner
                </a>
                &nbsp;|&nbsp;
                <a href="[LIEN_POLITIQUE]" style="color: #999999;">
                  Politique de confidentialité
                </a>
              </p>
            </td>
          </tr>

        </table>
        <!-- /CONTAINER -->

      </td>
    </tr>
  </table>
</body>
</html>
```

---

## ÉTAPE 2 — Templates spécialisés

### 2.1 Template campagne CPL (assurance/énergie/défiscalisation)

**Spécificités :**
- 1 seul CTA (formulaire de lead)
- Bénéfice immédiat en titre
- Pas d'images lourdes (rapidité de chargement)
- Conforme RGPD (mention opt-in visible)

**Structure recommandée :**
```
[Logo + nom expéditeur]
[Titre bénéfice fort : économisez X € / obtenez votre devis]
[3 arguments courts avec icône (ou bullet points)]
[CTA unique : "Je veux mon devis gratuit"]
[Paragraphe court sur la simplicité / rapidité]
[Preuve sociale : "X personnes ont déjà bénéficié..."]
[Footer légal + mention RGPD + désabonnement]
```

### 2.2 Template newsletter B2B (HB Digital)

**Spécificités :**
- Format "journal" — plusieurs sujets
- Header avec logo et numéro d'édition
- 2-3 blocs de contenu séparés
- Footer riche avec coordonnées et réseaux

**Structure :**
```
[Header : Logo HB Digital + "Newsletter #N — Mois AAAA"]
[Intro : 2-3 phrases éditoriales]
[Bloc 1 : Actualité / tip du mois]
[Séparateur visuel]
[Bloc 2 : Ressource ou guide]
[Séparateur visuel]
[Bloc 3 : Offre ou CTA]
[Footer : coordonnées + LinkedIn + désabonnement]
```

### 2.3 Template e-commerce (SEYDI Paris)

**Spécificités :**
- Image produit haute qualité (obligatoire)
- Ton aspirationnel
- Bouton "Découvrir / Commander"
- Design épuré, beaucoup d'espace

**Structure :**
```
[Header SEYDI Paris minimaliste]
[Image produit / collection pleine largeur]
[Titre émotionnel : "La nouvelle collection est arrivée"]
[Description courte — sensorielle]
[2 produits en colonnes avec prix et bouton]
[CTA principal : "Découvrir la collection"]
[Footer sobre avec réseaux et désabonnement]
```

---

## ÉTAPE 3 — Variables dynamiques

### 3.1 Syntaxe selon ESP

| ESP | Variable | Exemple |
|---|---|---|
| Brevo | `{{ contact.FIRSTNAME }}` | Bonjour {{ contact.FIRSTNAME }} |
| Mailjet | `{{var:firstname}}` | Bonjour {{var:firstname}} |
| Klaviyo | `{{ first_name }}` | Bonjour {{ first_name }} |
| Mailchimp | `*|FNAME|*` | Bonjour *|FNAME|* |

### 3.2 Variables standards à intégrer dans les templates

```
[PRENOM] → personnalisation salutation
[EMAIL] → lien de désabonnement
[DATE] → date d'envoi si utile
[LIEN_OFFRE] → URL principale trackée
[LIEN_DESABO] → obligatoire légalement
[PREHEADER] → texte de prévisualisation (hidden, haut du body)
```

---

## ÉTAPE 4 — Checklist avant envoi

### 4.1 Technique

- [ ] Largeur max 600px respectée ?
- [ ] Toutes les images ont un alt text ?
- [ ] Tous les liens sont absolus et trackés (UTM) ?
- [ ] Lien de désabonnement fonctionnel ?
- [ ] Poids total email < 100ko ?
- [ ] Test rendu Outlook + Gmail + mobile effectué ?

### 4.2 Légal et délivrabilité

- [ ] Identité expéditeur claire (from name + from email) ?
- [ ] Mention "publicité" si email commercial ? (selon réglementation)
- [ ] RGPD : email envoyé uniquement à des opt-in ?
- [ ] Ratio texte/images > 60% texte ?
- [ ] Pas de spam words dans l'objet (gratuit, urgent, exclusif en majuscules) ?

---

## FORMAT DE SORTIE

```
## Template Email — [Type] — [Projet]

**ESP cible :** [Brevo / Mailjet / SES / Universel]
**Variables dynamiques :** [liste]
**Responsive :** [Oui / Non]

---

[CODE HTML COMPLET]

---

**Placeholders à compléter :**
- [LOGO_URL] : URL du logo
- [COULEUR_PRIMAIRE] : ex. #2563EB
- [TEXTE_CTA] : ex. "Obtenir mon devis"
- [URL_CTA] : lien + UTM

**Tests recommandés :** Litmus / Email on Acid / Gmail direct
**Prochaine étape :** [intégrer dans ESP / envoyer test / valider avec client]
```

---

## RÈGLES ABSOLUES

1. Structure TABLES uniquement — jamais de divs pour la mise en page
2. CSS inline obligatoire — sauf media queries mobile
3. Lien de désabonnement dans chaque email (obligation légale)
4. Tester sur Outlook (le pire cas) avant tout envoi
5. Finir par la liste des placeholders à compléter + le next step
