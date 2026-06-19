---
name: commercial-forecaster
description: >
  Forecaster commercial pour HB Digital. Déclenche sur : prévision CA,
  objectif mensuel, projection pipeline, estimation revenus, forecast
  affiliation, prévision leads, plan commercial, objectif trimestriel,
  simulation budget, prévision par activité, revue pipeline, deal probabilisé.
  Couvre les 3 activités HB Digital : Lead Gen, Affiliation, Distribution.
  Self-healing : produit une projection même avec des données partielles,
  en documentant les hypothèses retenues.
---

# Commercial Forecaster — HB Digital Performance

## Contexte

| Activité | Prévisibilité | Facteurs clés |
|---|---|---|
| **Consulting / Lead Gen** | Moyenne | Clients actifs, budget géré, saisonnalité |
| **Affiliation / Monétisation** | Faible-Moyenne | Plateformes actives, performances campagnes |
| **Distribution magazines** | Élevée | Contrats collectivités, BPU fixes |

**Historique de référence :**

| Mois | CA Consulting | CA Distribution | CA Monétisation | Total |
|---|---|---|---|---|
| Jan 2026 | 14 572 € | 0 € | 0 € | 14 572 € |
| Fév 2026 | 13 291 € | 0 € | 0 € | 13 291 € |
| Mar 2026 | 3 953 € | 2 457 € | 0 € | 6 410 € |
| **Moyenne 3 mois** | **~10 605 €** | **~819 €** | **~0 €** | **~11 424 €** |

> Cette table s'enrichit à chaque clôture.

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Pipeline non fourni | Utiliser moyennes historiques + signaler |
| Horizon non précisé | Forecast M+1 par défaut |
| Activité non précisée | Forecaster les 3 activités séparément |
| Données partielles | Extrapoler + documenter hypothèses |
| Nouvelle activité sans historique | Partir de 0, construire depuis les deals en cours |

---

## ÉTAPE 1 — Collecte des inputs

### 1.1 Pipeline deals en cours

Pour chaque deal, collecter :

| Deal | Activité | Valeur estimée | Probabilité | Date de closing |
|---|---|---|---|---|
| [Nom client A] | Consulting | XX € | XX% | [date] |
| [Nom client B] | Leads | XX € | XX% | [date] |
| [Collectivité C] | Distribution | XX € | XX% | [date] |

**Probabilités par défaut selon stade :**

| Stade deal | Probabilité |
|---|---|
| Prospect identifié | 5-10% |
| Prise de contact effectuée | 15-25% |
| Proposition envoyée | 35-50% |
| Négociation en cours | 60-75% |
| Accord verbal | 85-95% |
| Bon de commande signé | 100% |

### 1.2 Revenus récurrents confirmés

Clients avec contrats actifs (revenus quasi-certains) :

| Client | Activité | Montant mensuel | Fin de contrat |
|---|---|---|---|
| [Client récurrent 1] | | XX € | [date] |
| [Client récurrent 2] | | XX € | [date] |

---

## ÉTAPE 2 — Construction du forecast

### 2.1 Méthode de calcul

```
CA FORECAST M+1 =

REVENUS CERTAINS
├── Contrats actifs reconductibles      XX €  (probabilité 90%)
└── Bons de commande signés             XX €  (probabilité 100%)
= Sous-total certain                    XX €

REVENUS PROBABLES
├── Négociation avancée × proba         XX €
└── Propositions envoyées × proba       XX €
= Sous-total probable                   XX €

REVENUS ESPÉRÉS
├── Nouvelles opportunités × proba      XX €
└── Upsell clients existants × proba    XX €
= Sous-total espéré                     XX €

CA FORECAST TOTAL                       XX €
```

### 2.2 Trois scénarios

| Scénario | Hypothèse | Calcul |
|---|---|---|
| **Pessimiste** | Seuls les revenus certains se concrétisent | Certain × 90% |
| **Base** | Certain + 60% des probables | Certain + Probable × 60% |
| **Optimiste** | Tout se concrétise + 1 surprise | Certain + Probable + 50% Espéré |

### 2.3 Forecast par activité

**Consulting / Lead Gen :**
```
Clients actifs en cours : XX € (récurrent confirmé)
+ Nouveaux deals pipeline : XX € × probabilité
+ Upsell possible : XX €
= Forecast Consulting : XX € (base) / XX € (pessimiste) / XX € (optimiste)
```

**Affiliation / Monétisation :**
```
Revenus plateformes actives (moyenne 3 mois) : XX €
± Variation campagnes en cours : XX €
= Forecast Affiliation : XX € (base)
Note : haute volatilité — fourchette ±30%
```

**Distribution magazines :**
```
Marchés actifs confirmés : XX €
+ AO en cours × probabilité : XX €
= Forecast Distribution : XX € (haute certitude si contrats signés)
```

---

## ÉTAPE 3 — Analyse des écarts

### 3.1 Comparaison forecast vs réalisé

```
| Mois | Forecast base | Réalisé | Écart € | Écart % | Cause principale |
|---|---|---|---|---|---|
| [M-2] | XX € | XX € | XX € | XX% | [analyse] |
| [M-1] | XX € | XX € | XX € | XX% | [analyse] |
```

### 3.2 Calibration des probabilités

Si les deals "négociation avancée" (75%) se concrétisent à 50% en réalité → recalibrer à 50% pour les prochains forecasts.

**Ajustement automatique :** après 3 mois de données, recalibrer les probabilités par stade en fonction du taux de conversion réel observé.

---

## ÉTAPE 4 — Plan d'actions commercial

### 4.1 Gap analysis

```
Objectif mensuel : XX €
Forecast base     : XX €
GAP               : XX €

Pour combler le gap :
- Accélérer X deal(s) en négociation → +XX €
- Relancer Y prospects inactifs → +XX €
- Upsell Z clients actifs → +XX €
```

### 4.2 Actions prioritaires par semaine

```
Semaine 1 : Relancer tous les deals "proposition envoyée" > 7 jours sans réponse
Semaine 2 : Soumettre 3 nouvelles propositions (pipeline froid)
Semaine 3 : Revue upsell clients actifs — identifier 1 opportunité concrète
Semaine 4 : Clôturer ou disqualifier les deals > 30 jours en pipeline
```

---

## FORMAT DE SORTIE

```
## Forecast Commercial — [Période]
Généré le : [DATE]

**Vue d'ensemble :**
| Scénario | CA estimé | Probabilité |
|---|---|---|
| Pessimiste | XX € | Certain |
| Base | XX € | Probable |
| Optimiste | XX € | Ambitieux |

**Par activité (scenario base) :**
| Activité | Forecast | Récurrent | Nouveau |
|---|---|---|---|
| Consulting / Lead Gen | XX € | XX € | XX € |
| Affiliation | XX € | XX € | XX € |
| Distribution | XX € | XX € | XX € |
| **TOTAL** | **XX €** | **XX €** | **XX €** |

**Top 3 deals à clôturer en priorité :**
1. [Client A] — XX € — [action à faire]
2. [Client B] — XX € — [action à faire]
3. [Client C] — XX € — [action à faire]

**Gap vs objectif :** XX € → [action pour combler]

**Prochaine étape :** [action précise + date]
```

---

## RÈGLES ABSOLUES

1. Toujours présenter 3 scénarios (pessimiste / base / optimiste)
2. Documenter chaque hypothèse retenue
3. Séparer revenus récurrents (prévisibles) des revenus nouveaux (incertains)
4. Recalibrer les probabilités après chaque mois — jamais de valeurs figées
5. Finir par un gap analysis + 3 actions concrètes pour atteindre l'objectif
