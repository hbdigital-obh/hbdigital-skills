---
name: site-architecture
description: >
  Architecte de sites web et structure d'information pour HB Digital. Déclenche
  sur : arborescence, structure de site, plan de site, sitemap, navigation,
  maillage interne, UX structure, wireframe, menu, page à créer, organisation
  du site, refonte structure, pages nécessaires, hiérarchie de pages. Couvre :
  sites lead gen, sites de contenu, landing pages, sites e-commerce, sites
  agence. Self-healing : produit une architecture même sans brief complet,
  calibre selon le type de site et l'objectif détectés.
---

# Site Architecture — HB Digital Performance

## Contexte sites HB Digital

| Site | Type | Objectif principal | Stack |
|---|---|---|---|
| `hbdigital.fr` | Site agence | Lead B2B + crédibilité | WordPress |
| `seydiparis.com` | E-commerce mode | Vente en ligne | Shopify |
| `etude-defisc.fr` | Site lead gen | Capture leads défiscalisation | WordPress / statique |
| `lacavernedesastuces.fr` | Site de contenu | Trafic SEO + monétisation | WordPress |
| `topsmeilleurs.com` | Site comparatif | Trafic SEO + affiliation | WordPress |
| LPs campagnes | Landing pages | Conversion lead unique | HTML statique / WP |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Objectif non précisé | Demander "quel est le but principal du site ?" |
| Stack non précisée | Recommander WordPress (polyvalent) sauf e-commerce (Shopify) |
| Secteur non précisé | Inférer depuis le contexte et proposer 3 structures standard |
| Budget non précisé | Proposer MVP d'abord, puis version évolutive |

---

## ÉTAPE 1 — Diagnostic du besoin

### 1.1 Questions fondamentales

```
1. Type de site : [lead gen / contenu SEO / e-commerce / agence / LP]
2. Objectif principal : [leads / ventes / trafic / crédibilité]
3. Audience : [B2B / B2C — caractéristiques]
4. Volume de pages : [5 / 20 / 100+]
5. Stack existante ou à choisir : [CMS / statique / Shopify]
6. Contrainte SEO : [oui — mots-clés cibles / non]
```

### 1.2 Déterminer le type d'architecture

| Type de site | Architecture dominante |
|---|---|
| LP single page | 1 page, sections verticales, 1 CTA |
| Site lead gen | 3-8 pages + LP dédiées par verticale |
| Site de contenu | Catégories + tags + articles (100-1 000 pages) |
| Site agence | Vitrine 5-10 pages + blog |
| E-commerce | Collections + produits + pages statiques |

---

## ÉTAPE 2 — Structures d'arborescence par type

### 2.1 Site agence / consulting (hbdigital.fr)

```
Niveau 0 — Page d'accueil
├── Services /services
│   ├── Lead Generation /services/lead-generation
│   ├── Affiliation /services/affiliation
│   ├── Consulting Trafic /services/consulting-trafic
│   └── Production Web /services/production-web
├── Références / Cas clients /references
├── Blog /blog
│   ├── Catégorie : Performance & Lead Gen
│   ├── Catégorie : Affiliation
│   └── Catégorie : Conseil digital
├── À propos /a-propos
└── Contact /contact

Pages légales (footer) :
├── Mentions légales
├── Politique de confidentialité
└── CGV / CGU
```

### 2.2 Site lead gen (etude-defisc.fr)

```
Niveau 0 — Page d'accueil (= LP principale)
├── [Optionnel] Pages par dispositif fiscal :
│   ├── /lmnp
│   ├── /pinel
│   ├── /deficit-foncier
│   └── /denormandie
├── [Optionnel] Blog /conseils
│   └── Articles SEO informationnels
└── Mentions légales / Politique de confidentialité

Note : structure minimaliste, tout converge vers le formulaire.
Chaque sous-page = LP thématique avec son propre formulaire.
```

### 2.3 Site de contenu SEO (lacavernedesastuces.fr / topsmeilleurs.com)

```
Niveau 0 — Page d'accueil
├── Catégories (niveau 1)
│   ├── /categorie-1
│   │   ├── /sous-categorie-1-1
│   │   └── /sous-categorie-1-2
│   └── /categorie-2
│       └── ...
├── Articles (niveau 2 ou 3 selon profondeur)
│   └── /categorie/sous-categorie/nom-article
├── À propos /a-propos
└── Contact / Pages légales

Règle SEO : max 3 clics depuis la home vers tout article.
```

### 2.4 E-commerce (seydiparis.com)

```
Niveau 0 — Page d'accueil
├── Collections /collections
│   ├── /collections/robes
│   ├── /collections/hauts
│   ├── /collections/pantalons
│   └── /collections/accessoires
├── Produits /products/[slug]
├── Notre histoire /pages/notre-histoire
├── Nos valeurs /pages/nos-valeurs
├── Blog /blogs/actualites
├── Outlet / Promotions /pages/outlet (optionnel)
└── FAQ / Contact / Livraisons / Retours (footer)
```

### 2.5 Landing page campaign (structure unique)

```
Structure sections (mono-page verticale) :

1. HERO — Promesse + CTA principal (above the fold)
2. PROBLÈME — Pain points de l'audience
3. SOLUTION — L'offre et ses bénéfices
4. PREUVES — Témoignages / chiffres / logos
5. COMMENT ÇA MARCHE — Process en 3 étapes
6. URGENCE — Raison d'agir maintenant
7. CTA FINAL — Formulaire ou bouton
8. FAQ — 3-5 questions fréquentes
9. FOOTER LÉGAL — Mentions + RGPD

Règle : 1 seul CTA visible à tout moment (répété en haut, milieu, bas).
Supprimer la navigation — aucune sortie de la page.
```

---

## ÉTAPE 3 — Maillage interne

### 3.1 Principes du maillage

```
RÈGLES FONDAMENTALES :
- Toute page doit être accessible en max 3 clics depuis la home
- Chaque page importante reçoit au moins 3 liens internes
- La home pointe vers les pages stratégiques (pas toutes les pages)
- Éviter les pages orphelines (aucun lien entrant)
- Ancres de liens descriptives (mot-clé SEO, pas "cliquez ici")
```

### 3.2 Matrice de maillage prioritaire

**Pour un site de contenu :**

```
Page pilier → reçoit des liens de tous les clusters
Page cluster → envoie un lien vers le pilier + vers autres clusters
Article → envoie 2-3 liens vers clusters/pilier + 1 lien vers CTA/LP

Exemple :
  Pilier : "Guide complet du lead gen assurance"
  Cluster : "CPL assurance auto" → lien vers pilier
  Cluster : "Qualification lead assurance" → lien vers pilier
  Article : "5 erreurs CPL assurance" → liens vers 2 clusters + vers pilier
```

### 3.3 Priorité de maillage (site lead gen)

```
High priority :
  Blog articles → LP de conversion correspondante
  Home → toutes les LP par verticale

Medium priority :
  LP verticale A → LP verticale B (cross-sell)
  About → Contact

Low priority :
  Footer → pages légales (obligatoire mais peu de valeur SEO)
```

---

## ÉTAPE 4 — Recommandations techniques

### 4.1 URLs propres

```
✅ Bon : /conseils/lead-gen/comment-generer-leads-assurance
❌ Mauvais : /p=1234 ou /index.php?cat=3&id=45

Règles :
- Tout en minuscules
- Tirets entre les mots (pas d'espaces, pas d'underscores)
- Mot-clé SEO principal dans l'URL
- Max 3-4 segments de profondeur
```

### 4.2 Structure des métas par type de page

| Type de page | Priorité title | Structure |
|---|---|---|
| Home | Haute | [Marque] — [Bénéfice principal] | [Mot-clé] |
| Page service/produit | Haute | [Mot-clé] — [Bénéfice] | [Marque] |
| Article blog | Haute | [Mot-clé] : [Titre accrocheur] |
| LP conversion | Moyenne | [Bénéfice] — [Offre] | [Marque] |
| Page légale | Basse | [Titre légal] — [Marque] |

---

## FORMAT DE SORTIE

```
## Architecture — [Nom du site]

**Type :** [lead gen / contenu / e-commerce / agence / LP]
**Objectif :** [conversion / trafic / crédibilité]
**Pages total estimées :** X pages

**Arborescence :**
[structure hiérarchique complète]

**Pages prioritaires à créer en premier :**
1. [Page] — [Pourquoi en priorité]
2. [Page] — [Pourquoi]
3. [Page] — [Pourquoi]

**Maillage interne clé :**
[3-5 règles de maillage spécifiques au projet]

**À ne pas faire :**
[2-3 erreurs spécifiques à éviter]

**Prochaine étape :** [créer sitemap / démarrer avec X pages / auditer l'existant]
```

---

## RÈGLES ABSOLUES

1. Toujours partir de l'objectif (conversion) et remonter vers la structure
2. MVP d'abord — une LP qui convertit vaut plus qu'un site de 50 pages vides
3. Max 3 clics depuis la home vers toute page importante
4. 1 page = 1 intention SEO = 1 audience — ne pas diluer
5. Finir par une liste de pages à créer en ordre de priorité
