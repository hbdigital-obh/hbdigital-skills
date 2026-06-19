---
name: pricing-strategist
description: >
  Stratège pricing pour HB Digital Performance. Déclenche sur : tarification,
  grille tarifaire, pricing leads, CPL, CPM, CPA, commission affilié, marge
  objectif, pricing prestation consulting, devis, bon de commande, valorisation
  d'offre, augmentation de prix, remise, pricing compétitif, rentabilité par
  offre. Couvre les 3 activités : Lead Gen / Affiliation / Distribution.
  Self-healing : ne bloque jamais sur une donnée manquante, propose une
  hypothèse chiffrée et continue.
---

# Pricing Strategist — HB Digital Performance

## Contexte pricing HB Digital

| Activité | Modèle dominant | Variables clés |
|---|---|---|
| **Lead Gen** | CPL (coût par lead) | Secteur, qualité lead, volume, exclusivité |
| **Affiliation** | CPA / Revenue Share | Taux conversion, ticket moyen, LTV client |
| **Consulting trafic** | Forfait ou % dépenses | Budget géré, résultats, fréquence reporting |
| **Production (LP, HTML)** | Forfait fixe | Complexité, délai, itérations |
| **Distribution magazines** | Prix unitaire × volume | Coût logistique, BPU collectivité |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Marge cible non précisée | Appliquer cible HB Digital : > 30% par défaut |
| Secteur inconnu | Demander 1 seule question, continuer avec benchmarks généraux |
| Volume non précisé | Calculer pour 3 paliers : 100 / 500 / 1 000 unités |
| Données concurrents manquantes | Estimer depuis les prix connus du marché, signaler *"estimation marché"* |

---

## ÉTAPE 1 — Analyse de la demande de pricing

### 1.1 Qualifier la situation

Avant toute recommandation, identifier :
- **Objet** : nouveau produit / révision tarifaire / réponse à un devis entrant ?
- **Marché** : annonceur, affilié, collectivité, PME cliente ?
- **Contrainte principale** : marge minimale, alignement concurrentiel, volume cible ?

### 1.2 Structure de coût à reconstituer

```
Coût direct =
  Coût acquisition trafic (si applicable)
+ Coût traitement / qualification lead
+ Coût production (LP, HTML, setup)
+ Quote-part charges fixes HB Digital

Marge brute = Prix de vente − Coût direct
Taux de marge = Marge / Prix de vente × 100
```

---

## ÉTAPE 2 — Modèles de pricing par activité

### 2.1 Pricing leads (Lead Gen CPL)

**Formule de base :**
```
CPL min viable = (Coût acq. trafic + Coût ops) / (Taux de conversion × (1 − Marge cible))

Exemple :
  Coût acq. trafic : 8 €/lead généré
  Coût ops : 2 €/lead
  Taux de conversion : 20%
  Marge cible : 30%
  → CPL mini = (8+2) / (1 − 0,30) = 14,30 €
```

**Grille CPL par secteur (benchmarks marché) :**

| Secteur | CPL bas | CPL moyen | CPL haut | Facteurs premium |
|---|---|---|---|---|
| Défiscalisation immobilière | 15 € | 35 € | 80 € | Qualification projet, revenus déclarés |
| Assurance auto | 8 € | 18 € | 35 € | Profil conducteur, véhicule |
| Assurance habitation | 5 € | 12 € | 25 € | Propriétaire vs locataire |
| Énergie (gaz/élec) | 6 € | 14 € | 28 € | Consommation estimée |
| Rénovation / pompe à chaleur | 20 € | 55 € | 120 € | Surface, profil acquéreur |
| Crédit immobilier | 25 € | 60 € | 150 € | Projet, apport, revenus |

**Critères de majoration :**
- Exclusivité lead : +30% à +80%
- Double opt-in confirmé : +20%
- Numéro vérifié : +15%
- Délai livraison < 24h : +10%

### 2.2 Pricing affiliation (CPA / RevShare)

**CPA — formule de valorisation :**
```
CPA acceptable pour l'annonceur =
  Ticket moyen × Taux de conversion pipeline × (1 − Coût variable)

CPA minimal pour HB Digital =
  Coût acquisition trafic affilié / Taux conversion campagne
```

**RevShare recommandé par secteur :**

| Secteur | RevShare bas | RevShare cible |
|---|---|---|
| E-commerce généraliste | 5% | 8-12% |
| Finance / assurance | 10% | 15-25% |
| Formation en ligne | 20% | 30-40% |
| Logiciel SaaS | 15% | 25-35% |

### 2.3 Pricing consulting / gestion trafic

**3 structures possibles :**

| Structure | Quand l'utiliser | Tarif indicatif HB Digital |
|---|---|---|
| **Forfait mensuel** | Relation récurrente, budget stable | 800 € à 3 500 €/mois selon périmètre |
| **% budget géré** | Budget important, scalabilité | 8% à 15% des dépenses média |
| **Hybride** | Nouveau client | Forfait mini + intéressement sur perf |

**Inclure systématiquement dans le forfait :**
- Setup (1 fois) : 500 € à 2 000 €
- Reporting mensuel : inclus
- Optimisations : X itérations/mois définies

### 2.4 Pricing production (LP, kits HTML, sites)

**Grille de référence :**

| Livrable | Prix bas | Prix cible | Prix haut |
|---|---|---|---|
| Landing page simple (1 bloc) | 400 € | 800 € | 1 500 € |
| Landing page optimisée (+ A/B, tracking) | 800 € | 1 500 € | 3 000 € |
| Kit HTML email (template master) | 300 € | 600 € | 1 200 € |
| Site vitrine 5 pages | 1 500 € | 3 500 € | 8 000 € |
| Intégration tracking complet | 300 € | 700 € | 1 500 € |

---

## ÉTAPE 3 — Grille tarifaire structurée

### Format de grille à produire

```
GRILLE TARIFAIRE — [ACTIVITÉ] — [DATE]

| Offre | Description | Volume | Prix unitaire | Remise vol. | Prix HT |
|---|---|---|---|---|---|
| [Nom offre 1] | ... | [palier] | XX € | -X% | XX € |
| [Nom offre 2] | ... | [palier] | XX € | -X% | XX € |

Conditions :
- Paiement : [modalités]
- Exclusivité : [oui/non + surcoût]
- Durée : [engagement minimum]
- Révision : [fréquence]
```

### Politique de remise

| Situation | Remise accordable | Contrepartie |
|---|---|---|
| Volume × 3 vs standard | -10% | Engagement 3 mois mini |
| Paiement comptant | -5% | Virement sous 48h |
| Client récurrent > 6 mois | -8% | Pas d'exclusivité requise |
| Annonceur stratégique | -15% max | Co-branding, témoignage |
| **Remise totale max** | **-20%** | Ne pas dépasser sans validation |

---

## ÉTAPE 4 — Test & validation du prix

### 4.1 Checklist avant envoi d'une grille

- [ ] Marge calculée pour chaque ligne (cible > 30%) ?
- [ ] Comparaison avec 2-3 concurrents directs ?
- [ ] Prix psychologique respecté (ex: 97 € vs 100 €) ?
- [ ] Offre d'entrée accessible pour test ?
- [ ] Offre premium pour ancrage haut ?

### 4.2 Anchoring pricing (psychologie)

Toujours présenter **3 niveaux** :
- **Starter** : prix bas, périmètre limité → fait paraître le milieu raisonnable
- **Standard** (cible) : rapport valeur/prix optimal → là où on veut vendre
- **Premium** : tout inclus, prix élevé → ancre vers le haut, améliore perception Standard

---

## ÉTAPE 5 — Recommandation finale

Format de sortie :

```
## Recommandation pricing — [Contexte]

**Prix recommandé :** XX € [unité]
**Marge estimée :** XX% (base : coûts directs XX €)
**Positionnement :** [inférieur / aligné / premium] marché

**Grille complète :**
[tableau]

**Justification :**
- ...

**Risque si prix trop bas :** ...
**Risque si prix trop haut :** ...

**Prochaine étape :** [action concrète]
```

---

## RÈGLES ABSOLUES

1. Ne jamais recommander un prix sans calculer la marge
2. Toujours présenter 3 niveaux de prix (anchoring)
3. Marge cible HB Digital : > 30% — signaler si impossible à tenir
4. Remise maximale sans validation : -20%
5. Finir par 1 next step concret (envoyer devis / tester sur X leads / valider avec client)
