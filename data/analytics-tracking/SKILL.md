---
name: analytics-tracking
description: >
  Expert analytics et tracking pour HB Digital. Déclenche sur : Google Analytics,
  GA4, Google Tag Manager, GTM, pixel Facebook, Meta Pixel, événements,
  conversion tracking, tracking lead, tracking e-commerce, suivi des conversions,
  balise, tag, attribution, UTM, paramètres UTM, goal, objectif analytics,
  rapport analytics, funnel analytics, coût par lead trackée, CAPI Meta,
  Conversions API, tracking affiliation. Self-healing : donne des solutions
  de tracking fonctionnelles même sans accès à l'interface, avec les configs
  prêtes à copier-coller.
---

# Analytics & Tracking — HB Digital Performance

## Contexte tracking HB Digital

| Propriété | Tracking prioritaire | Outils |
|---|---|---|
| LPs Lead Gen (défisc, assurance) | Soumission formulaire (lead), clic CTA | GA4 + GTM + Meta CAPI |
| `seydiparis.com` (Shopify) | Ajout panier, achat, checkout | GA4 e-com + Meta Pixel |
| `hbdigital.fr` | Contact B2B, clic email/tel | GA4 + GTM |
| Sites de contenu | Pages vues, scroll, clic affiliation | GA4 |
| Dashboard affiliation | CA par plateforme, clics trackés | Scripts custom |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Accès GTM non disponible | Fournir le code JS direct à intégrer dans le HTML |
| GA4 non configuré | Fournir la procédure de setup de base |
| CMS non précisé | Donner la solution WordPress + la solution HTML statique |
| Événement non défini | Identifier l'événement le plus proche GA4 standard |

---

## ÉTAPE 1 — Stack de tracking recommandée

### 1.1 Architecture standard HB Digital

```
COUCHE 1 : Collecte des données
├── Google Analytics 4 (GA4) — données site, audiences, conversions
├── Google Tag Manager (GTM) — chef d'orchestre de tous les tags
└── Meta Pixel / CAPI — données pub Facebook/Instagram

COUCHE 2 : Activation des données
├── Google Ads — conversions importées depuis GA4
├── Meta Ads — événements envoyés via Pixel + CAPI (redundant)
└── Plateforme d'affiliation — pixels de conversion tiers

COUCHE 3 : Reporting
├── Looker Studio — dashboard consolidé
└── GA4 + Meta Ads Manager — analyse par canal
```

### 1.2 Setup prioritaire par site

| Site | Priorité 1 | Priorité 2 | Priorité 3 |
|---|---|---|---|
| LP Lead Gen | GTM + event form_submit | Meta Pixel + LeadEvent | UTMs structurés |
| SEYDI Paris | GA4 e-commerce | Meta Pixel + Purchase | Klaviyo tracking |
| hbdigital.fr | GTM + contact | GA4 goals | LinkedIn Insight Tag |
| Sites contenu | GA4 page views | Scroll depth | Clic liens affiliés |

---

## ÉTAPE 2 — Configurations prêtes-à-déployer

### 2.1 Installation GA4 via GTM

**Étape 1 — Créer le tag GA4 Configuration dans GTM :**
```
Tag type : Google Analytics: GA4 Configuration
Measurement ID : G-XXXXXXXXXX
Trigger : All Pages
```

**Étape 2 — Créer l'événement de conversion (form submit) :**
```
Tag type : Google Analytics: GA4 Event
Event Name : generate_lead
Event Parameters :
  form_id : {{Click ID}} ou {{Form ID}}
  page_location : {{Page URL}}
Trigger : Form Submit (configurer le trigger ci-dessous)
```

**Trigger Form Submit dans GTM :**
```
Trigger type : Form Submission
Wait for Tags : Checked
Check Validation : Checked
Fire On : All Forms OU Some Forms
  Condition : Form ID = [ID du formulaire]
  OU : Page URL contains /merci (thank you page)
```

### 2.2 Thank you page tracking (méthode alternative)

Si le formulaire redirige vers une page `/merci` :

```html
<!-- À placer sur la page /merci UNIQUEMENT -->
<!-- GA4 - Conversion lead -->
<script>
  gtag('event', 'generate_lead', {
    'event_category': 'form',
    'event_label': '[Nom du formulaire]',
    'value': 1
  });
</script>

<!-- Meta Pixel - Lead event -->
<script>
  fbq('track', 'Lead');
</script>
```

### 2.3 Meta Pixel — Configuration complète

**Code d'installation de base (dans <head>) :**
```html
<!-- Meta Pixel Code -->
<script>
!function(f,b,e,v,n,t,s)
{if(f.fbq)return;n=f.fbq=function(){n.callMethod?
n.callMethod.apply(n,arguments):n.queue.push(arguments)};
if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
n.queue=[];t=b.createElement(e);t.async=!0;
t.src=v;s=b.getElementsByTagName(e)[0];
s.parentNode.insertBefore(t,s)}(window, document,'script',
'https://connect.facebook.net/en_US/fbevents.js');
fbq('init', '[PIXEL_ID]');
fbq('track', 'PageView');
</script>
<noscript>
  <img height="1" width="1" style="display:none"
  src="https://www.facebook.com/tr?id=[PIXEL_ID]&ev=PageView&noscript=1"/>
</noscript>
```

**Événements Meta à tracker pour lead gen :**
```javascript
// Affichage LP
fbq('track', 'ViewContent', {content_name: '[Nom LP]'});

// Clic sur CTA (déclenchement formulaire)
fbq('track', 'InitiateCheckout');

// Soumission formulaire (sur la thank you page ou au submit)
fbq('track', 'Lead', {
  content_name: '[Nom de l\'offre]',
  content_category: '[Secteur]'
});
```

### 2.4 UTM — Structure standardisée HB Digital

**Convention UTM à appliquer sur toutes les URLs de campagne :**

```
utm_source   = [plateforme] : facebook / google / brevo / affiliation / linkedin
utm_medium   = [type de media] : cpc / email / organic / display / referral
utm_campaign = [nom campagne] : [secteur]-[offre]-[date] ex: defisc-pinel-2024q4
utm_content  = [variante créative] : ad1 / ad2 / banner_300x250
utm_term     = [mot-clé] : (pour Google Ads principalement)
```

**Générateur UTM en ligne :** ga-dev-tools.google.com/campaign-url-builder

**Tableau de suivi des UTMs (Google Sheets) :**
```
| Campagne | Plateforme | URL de base | UTM complet | Date | Statut |
|---|---|---|---|---|---|
| [nom] | Facebook | [url] | [url?utm=...] | [date] | Active |
```

### 2.5 Tracking clics liens affiliés

**Pour tracker les clics sortants vers des offres affiliées :**

```javascript
// Coller dans le head ou GTM
document.addEventListener('click', function(e) {
  var link = e.target.closest('a');
  if (!link) return;
  
  var href = link.getAttribute('href');
  if (!href) return;
  
  // Tracker les clics sur liens externes
  if (href.indexOf('[DOMAINE_AFFILIEUR]') > -1) {
    gtag('event', 'affiliate_click', {
      'event_category': 'affiliation',
      'event_label': href,
      'link_url': href
    });
    
    // Meta Pixel si applicable
    if (typeof fbq !== 'undefined') {
      fbq('trackCustom', 'AffiliateClick', {url: href});
    }
  }
});
```

---

## ÉTAPE 3 — Configuration GA4 conversions

### 3.1 Événements à marquer comme conversions

Dans GA4 Admin → Events → Mark as conversion :

| Événement | Priorité | Valeur |
|---|---|---|
| `generate_lead` | +++++ | 1 (ou valeur CPL) |
| `purchase` (Shopify) | +++++ | Valeur de la transaction |
| `contact` | +++ | 1 |
| `affiliate_click` | ++ | 1 |
| `scroll` (90%) | + | Indicatif |

### 3.2 Audiences GA4 à créer

```
Pour remarketing et analyse :

1. "A soumis le formulaire" — Event = generate_lead (30 derniers jours)
2. "A visité la LP sans convertir" — A visité [URL LP] SANS generate_lead
3. "Visiteurs engagés" — Scroll > 75% ou temps > 2 min
4. "Source paid" — Session medium = cpc
```

---

## ÉTAPE 4 — Reporting analytics

### 4.1 KPIs à suivre par type de site

**Lead Gen :**
```
| KPI | Formule | Cible |
|---|---|---|
| Taux de conversion | Leads / Sessions × 100 | > 5% |
| CPL Google Ads | Coût / Leads | Selon secteur |
| CPL Meta | Coût / Leads | Selon secteur |
| Taux rebond LP | % sessions 1 page | < 60% |
| Source top | Canal générant + de leads | --- |
```

**E-commerce (SEYDI) :**
```
| KPI | Formule | Cible |
|---|---|---|
| Taux conv. achat | Transactions / Sessions | > 2% |
| Taux add-to-cart | Ajouts / Vues produits | > 10% |
| Taux checkout | Checkouts / Add-to-cart | > 50% |
| ROAS | CA / Dépenses pub | > 3× |
| Panier moyen | CA / Transactions | --- |
```

### 4.2 Rapport hebdomadaire automatisable

**Données à extraire chaque lundi matin :**
```
Via GA4 API ou export planifié :
- Sessions par canal (7 derniers jours vs semaine précédente)
- Leads générés par canal
- Taux de conversion par page d'entrée
- Top 5 pages de destination
```

---

## FORMAT DE SORTIE

### Setup tracking demandé

```
## Plan de tracking — [Projet]

**Objectif principal :** [Lead / Achat / Contact]
**Événement de conversion :** [generate_lead / purchase / contact]

**Checklist d'installation :**
□ GTM installé sur le site
□ GA4 configuré (Measurement ID : G-XXXXXX)
□ Événement de conversion créé dans GTM
□ Marqué comme conversion dans GA4
□ Meta Pixel installé (si applicable)
□ Event Lead déclenché sur thank you page
□ UTMs appliqués sur toutes les URLs de campagne
□ Test de validation effectué (GTM Preview Mode)

**Code à intégrer :**
[code prêt à copier]

**Vérification :**
[comment vérifier que ça fonctionne]

**Prochaine étape :** [action précise]
```

---

## RÈGLES ABSOLUES

1. Ne jamais lancer une campagne payante sans tracking de conversion fonctionnel
2. GTM est le chef d'orchestre — tous les tags passent par GTM
3. Toujours tester en GTM Preview Mode avant de publier
4. UTMs sur 100% des liens de campagnes — aucune exception
5. Finir par une checklist de validation testable dans les 30 minutes
