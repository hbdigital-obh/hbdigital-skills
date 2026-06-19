---
name: deal-desk
description: >
  Deal-desk opérationnel pour HB Digital. Déclenche sur : proposition
  commerciale, offre à envoyer, contrat, bon de commande, négociation en cours,
  deal à clôturer, conditions commerciales, devis à rédiger, terme d'un accord,
  clause de contrat, SLA, annexe technique, CGV, renouvellement, avenant.
  Couvre clients annonceurs, affiliés partenaires et collectivités.
  Self-healing : génère un document opérationnel même avec des informations
  partielles, en signalant les éléments à compléter.
---

# Deal-Desk — HB Digital Performance

## Contexte

Le deal-desk de HB Digital couvre 3 types de relations commerciales :

| Relation | Documents types | Enjeux clés |
|---|---|---|
| **HB Digital → Annonceur** | Contrat prestation, bon de commande leads, CGV | Clauses de volume, qualité lead, exclusivité |
| **HB Digital → Affilié** | Contrat partenariat, grille commission, charte éditeur | Protection données, exclusivité verticale, fraude |
| **HB Digital → Collectivité** | CCTP, BPU, bon de commande, avenant marché | Conformité marchés publics, délais paiement 30j |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Coordonnées client manquantes | Générer avec `[À COMPLÉTER : …]` |
| Montant non précisé | Créer un champ variable `[MONTANT]` avec note |
| Durée non précisée | Durée standard par type de deal (voir ci-dessous) |
| Droit applicable non précisé | France / Droit français par défaut |
| Demande floue | Identifier le type de document + poser 1 seule question |

---

## ÉTAPE 1 — Qualification du deal

### 1.1 Identifier le type de deal

```
DEAL ENTRANT → identifier :
1. Type de partie (annonceur / affilié / collectivité / prestataire)
2. Objet (leads / affiliation / prestation / production / distribution)
3. Durée (ponctuel / mensuel / annuel / tacite reconduction)
4. Volume (estimé si non précisé)
5. Mode de paiement (virement / CB / 30j fin de mois)
6. Niveau de risque (nouveau client = risque moyen / référence = faible)
```

### 1.2 Durées standard par type

| Type de deal | Durée standard | Tacite reconduction |
|---|---|---|
| Contrat leads annonceur | 3 mois | Oui, préavis 30j |
| Partenariat affilié | 12 mois | Oui, préavis 30j |
| Prestation consulting | 6 mois | Oui, préavis 15j |
| Production (LP/site) | Ponctuel | Non |
| Distribution collectivité | Durée du marché public | Non |

---

## ÉTAPE 2 — Templates de documents

### 2.1 Bon de commande leads (annonceur)

```
BON DE COMMANDE — LEADS

N° BC : [AUTO]             Date : [DATE]
Émetteur : HB Digital — SASU     SIRET : [À compléter]
Client : [NOM SOCIÉTÉ]           SIRET : [À compléter]

COMMANDE :
| Description | Volume | CPL | Montant HT |
|---|---|---|---|
| Leads [SECTEUR] — [CRITÈRES] | [N] leads | [X] € | [TOTAL] € |

Conditions de livraison :
- Format : [CSV / API / email]
- Délai : [X] jours ouvrés après validation
- Exclusivité : [Oui / Non]
- Critères de qualité : [liste]

Conditions de paiement :
- Règlement : [virement / CB]
- Échéance : [30j fin de mois / comptant]
- Pénalité retard : 3× taux légal

Acceptation :
Signature acheteur : _______________   Date : ___
Signature HB Digital : _______________   Date : ___
```

### 2.2 Contrat partenariat affilié

```
CONTRAT DE PARTENARIAT AFFILIÉ

Entre :
  HB Digital — SASU, ci-après "l'Opérateur"
  [NOM AFFILIÉ] — [Forme juridique], ci-après "l'Éditeur"

Objet :
  L'Éditeur génère du trafic qualifié vers les offres de l'Opérateur
  en contrepartie d'une rémunération à la performance.

Article 1 — Périmètre
  Verticales concernées : [LISTE]
  Zones géographiques : France métropolitaine

Article 2 — Rémunération
  Modèle : [CPA / RevShare / CPL]
  Taux / montant : [X] €/lead ou [X]% du CA généré
  Seuil de paiement : [50 €] minimum
  Fréquence : mensuelle, le [15] du mois suivant

Article 3 — Obligations de l'Éditeur
  - Respect de la charte qualité trafic HB Digital
  - Interdiction de trafic incentivé non déclaré
  - Interdiction de brand bidding sans accord écrit
  - Déclaration de toute co-opération avec annonceurs concurrents

Article 4 — Obligations de l'Opérateur
  - Mise à disposition des ressources promotionnelles
  - Reporting mensuel des stats
  - Paiement dans les délais contractuels

Article 5 — Données personnelles
  Chaque partie est responsable de traitement indépendant.
  Transfert de données conforme au RGPD.

Article 6 — Durée et résiliation
  Durée : 12 mois, renouvelable tacitement
  Préavis : 30 jours par lettre recommandée

Signatures : _______________         _______________
```

### 2.3 Conditions de qualité leads (annexe technique)

```
ANNEXE QUALITÉ — LEADS [SECTEUR]

Critères d'acceptation :
- [ ] Formulaire rempli de manière volontaire (opt-in RGPD)
- [ ] Numéro de téléphone vérifié format FR
- [ ] Email valide (syntaxe + MX)
- [ ] IP France / non proxy
- [ ] Âge : [18-70 ans]
- [ ] [Critère spécifique secteur]

Motifs de rejet (lead non dû) :
- Doublon dans les 30 jours
- Numéro incorrect ou inatteignable 3 relances
- Fausse identité prouvée
- Hors zone géographique

Taux de rejet maximum accepté : [15]%
Au-delà : déduction automatique sur facture du mois suivant.

Litige : traitement sous 5 jours ouvrés par email dédié.
```

---

## ÉTAPE 3 — Check-list avant envoi d'un deal

### 3.1 Vérification commerciale

- [ ] Prix et volumes cohérents avec la grille tarifaire ?
- [ ] Marge calculée et acceptable (> 30%) ?
- [ ] Remise éventuelle dans la limite autorisée (≤ 20%) ?
- [ ] Mode de paiement et délai clairement indiqués ?

### 3.2 Vérification juridique minimale

- [ ] SIRET des deux parties présent ?
- [ ] Clause de responsabilité limitée incluse ?
- [ ] Mention RGPD pour tout traitement de données ?
- [ ] Clause de résiliation avec préavis ?
- [ ] Droit applicable et juridiction compétente ?

### 3.3 Red flags — ne pas signer sans résoudre

- ⚠️ Délai de paiement > 60 jours → négocier à 30j ou exiger acompte
- ⚠️ Absence de critères de qualité leads → ajouter annexe technique
- ⚠️ Exclusivité sans surcoût → facturer +30% minimum
- ⚠️ Clause de non-concurrence large → restreindre à 6 mois / verticale spécifique
- ⚠️ Rémunération variable sans floor → exiger un minimum garanti

---

## ÉTAPE 4 — Négociation et closing

### 4.1 Lever les objections types

| Objection | Réponse |
|---|---|
| "C'est trop cher" | Montrer le ROI annonceur / rappeler les critères qualité |
| "On veut tester d'abord" | Proposer un pilote 30j, volume limité, sans engagement |
| "On a un fournisseur actuel" | Proposer un dual-sourcing — pas de risque, comparaison réelle |
| "Délai de paiement 60j" | Accepter si client stratégique + acompte 30% à la commande |
| "On veut l'exclusivité gratuite" | Expliquer le coût d'opportunité + proposer exclusivité partielle (zone/secteur) |

### 4.2 Stratégie de closing

```
Deal en négociation > 2 semaines :
→ Proposer une version "lite" à moindre engagement
→ Ajouter un bonus limité dans le temps ("offre valable 7 jours")
→ Envoyer un bon de commande pré-rempli pour réduire la friction
```

---

## FORMAT DE SORTIE

```
## Deal Summary — [Client] — [Objet]

**Statut :** [En négociation / À envoyer / Signé]
**Valeur estimée :** XX € HT / [durée]
**Marge estimée :** XX%

**Document joint :** [type de document]
**Éléments à compléter avant envoi :** [liste]
**Red flags identifiés :** [liste ou "Aucun"]

**Prochaine étape :** [action précise + deadline]
```

---

## RÈGLES ABSOLUES

1. Chaque document généré signale clairement les champs `[À COMPLÉTER]`
2. Ne jamais omettre les clauses RGPD sur tout traitement de données leads
3. Marge minimale 30% — si impossible, escalader avant de signer
4. Acompte obligatoire pour tout nouveau client > 2 000 € HT
5. Finir par 1 action concrète de closing
