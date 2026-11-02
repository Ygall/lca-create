---
name: lca-create
description: >
  Génère un sujet d'entraînement de lecture critique d'article (LCA) au format
  des EDN pour des étudiants en médecine de DFASM, à partir d'un article
  scientifique fourni en pièce jointe, d'un PMID ou d'un DOI. Produit un JSON
  structuré de QRU et QRM à cinq propositions, avec corrigé et justifications.
  À utiliser dès que l'utilisateur mentionne LCA, lecture critique d'article,
  EDN, ECNi, DFASM, externat, sujet d'entraînement sur un article, ou fournit un article avec une demande de
  questions, même sans employer le sigle LCA.
---

# lca-create

Construction d'un sujet de LCA calibré sur le format des EDN à partir d'un
article scientifique unique.

## Périmètre

Ce skill rédige des questions d'évaluation, pas un corrigé de méthodologie ni
une analyse critique rédigée. La sortie est un objet JSON unique conforme à
`assets/schema-sujet-lca.json`, importable dans une plateforme d'entraînement.

## Entrées acceptées et règle de dégradation

La rédaction de questions valides exige les sections Méthodes et Résultats
complètes : sans elles, l'essentiel des notions évaluables (schéma d'étude,
critère de jugement principal, calcul du nombre de sujets nécessaires,
population analysée, mesures d'association et précision) est inaccessible.

| Entrée | Conduite |
|---|---|
| Texte intégral (PDF, fichier texte, contenu collé) | Procéder directement. |
| PMID ou DOI | Récupérer les métadonnées et le résumé (MCP PubMed, à défaut recherche web). Si le texte intégral est accessible en libre accès, le récupérer et procéder. |
| PMID ou DOI sans texte intégral accessible | Ne pas générer le sujet. Indiquer que seul le résumé est disponible, préciser ce qui reste évaluable, et demander le texte intégral. Ne produire un sujet dégradé que si l'utilisateur le demande explicitement, en renseignant alors `controle_qualite.source_partielle = true`. |

Ne jamais inventer une donnée méthodologique absente du texte. Une question
dont la réponse n'est pas déterminable à partir du document est invalide.

## Paramètres

Extraire ces paramètres de la demande. Appliquer les valeurs par défaut sans
poser de question lorsque l'utilisateur ne les précise pas.

- `difficulte_cible` : entier de 1 à 10, défaut 5. Calibration détaillée dans
  `references/calibration-difficulte.md`.
- `objectifs_pedagogiques` : liste de notions à cibler prioritairement
  (par exemple biais de sélection, analyse en intention de traiter, NNT,
  validité externe). Défaut : couverture équilibrée de la grille du type
  d'étude. Lorsque des objectifs sont fournis, au moins 30 % des questions
  doivent s'y rattacher, le reste assurant la couverture minimale du texte.
  Un objectif peut désigner une notion du référentiel (par numéro, `id`,
  libellé ou terme anglais) ou rester formulé librement. Résoudre chaque
  objectif vers le référentiel (section suivante) et renseigner
  `parametres.notions_ciblees` ; un objectif sans équivalent dans le
  référentiel reste en texte libre dans `objectifs_pedagogiques`.
- `nombre_questions` : défaut 15. Valeurs admises 13 à 15. Choisir 15 sauf
  demande contraire ou article trop pauvre pour soutenir 15 questions non
  redondantes, auquel cas descendre à 13 et le signaler.

## Référentiel de notions

`assets/boussole_lca_notions.json` est la base de connaissance théorique du
skill : 143 notions de lecture critique (`niveau` base ou avance), chacune
avec `id`, `numero`, `libelle`, `description`, `prerequis`, `ouvre_vers` et
`termes_en`. Ce fichier est figé : ne jamais le modifier, ne jamais le
recopier dans la sortie, ne jamais inventer un `id` ou un `numero` absent du
fichier. Il propose une structuration pédagogique, pas le programme officiel.

- `id` est stable d'une version à l'autre ; `numero` (trois chiffres, par
  exemple 036) est recalculé à chaque version. Toujours citer le `numero` de
  la version du fichier effectivement lu.
- Recopier `projet`, `version`, `commit` et `date_version` du fichier dans
  `sujet.referentiel_notions`.
- Consulter sans charger le fichier entier. Index compact des notions :
  recherche multiligne en sortie `-o` du motif
  `"id": "[^"]+",\s+"numero": "\d+",\s+"libelle": "[^"]+"`, ou
  `jq -r '.notions[] | "\(.numero) \(.id) \(.libelle)"'` si `jq` est
  disponible. Lire ensuite le bloc des seules notions retenues (environ 40
  lignes à partir de leur `id`) pour leur `description`, leurs `prerequis`
  et leurs `termes_en`. À défaut d'outil de recherche, lire le fichier.

## Procédure

### Étape 1. Caractériser l'article

Avant toute rédaction, produire une fiche interne (non restituée à
l'utilisateur, sauf demande) comportant :

1. Type d'étude précis (essai randomisé, cohorte, cas-témoins, transversale,
   diagnostique, méta-analyse, médico-économique, qualitative).
2. Question de recherche formalisée (population, intervention ou exposition,
   comparateur, critère de jugement).
3. Critère de jugement principal et critères secondaires, avec leur nature.
4. Schéma de l'étude : randomisation, aveugle, appariement, période, centres.
5. Effectifs, calcul du nombre de sujets nécessaires, population d'analyse.
6. Méthodes statistiques, gestion des données manquantes, analyses en
   sous-groupes, multiplicité.
7. Résultats principaux chiffrés, mesures d'association et intervalles de
   confiance.
8. Contenu de la discussion, avec séparation des principaux résultats et de l'interprétation comparée aux autres études existantes   
9. Financement, conflits d'intérêts, enregistrement de l'essai.
10. Présence déclarées ou non déclarées de biais de sélection, de classement et de confusion
11. Limites déclarées 
12. Limites non déclarées repérables.

Cette fiche est l'unique source des questions : chaque proposition rédigée
ensuite doit être vérifiable dans le texte ou déductible de la fiche.
Il est aussi possible d'avoir des questions purement théoriques.
Elle doit être rendu en préambule du json pour audit.

### Étape 2. Sélectionner les notions

Lire `references/grilles-par-type-etude.md` et retenir la grille correspondant
au type d'étude identifié. Croiser avec `objectifs_pedagogiques`. Répartir les
notions retenues sur l'ensemble de la structure IMRaD, sans concentrer les
questions sur la seule section Méthodes.

Les notions doivent être distribuées sur l'introduction (rationnel, objectif) 
pour au moins 2 questions, les méthodes sur environ 5-6 questions, 
les résultats pour 4-5 et le reste sur la discussion.
Une question au minimum sur les biais, quelle que soit l'étude.
Il faut nécessairement une question d'ouverture et de perspective sur la conclusion à la toute fin (ce que cela implique)

Rattacher ensuite chaque notion retenue, et chaque objectif fourni, à son
entrée du référentiel (index de la section précédente). Lorsqu'une question
associe deux notions dépendantes, retenir aussi le prérequis (`prerequis`)
ou la notion qui s'en déduit (`ouvre_vers`). La grille par type d'étude
oriente le choix des notions ; le référentiel fournit leur formulation et leur
numéro. Une notion de la grille sans équivalent dans le référentiel peut être
évaluée, mais sans `notions` renseigné et avec une mention dans
`controle_qualite.reserves`.

### Étape 3. Rédiger les questions

Lire `references/regles-redaction.md` et appliquer ces règles intégralement.
Elles priment sur les indications résumées ci-dessous en cas de divergence.

Contraintes structurelles non négociables :

- Chaque question comporte exactement cinq propositions, notées A à E.
- Chaque question comporte au moins une proposition vraie. Une question sans
  proposition vraie est invalide.
- Le nombre de propositions vraies varie d'une question à l'autre selon la
  distribution cible ci-dessous. Une série où toutes les questions comportent
  deux ou trois propositions vraies est un échec de calibration.
- `type` vaut QRU lorsqu'une seule proposition est vraie, QRM sinon.
- Les questions suivent l'ordre de lecture de l'article. Aucune question ne
  doit révéler ni présupposer la réponse d'une autre.
- Chaque énoncé suit le gabarit fixe « N) Concernant [thème], quelle(s)
  est (sont) la (les) proposition(s) exacte(s) ? », détaillé dans
  `references/regles-redaction.md`.
- Chaque question porte sur un seul thème et appartient à une seule des
  trois familles définies dans `references/regles-redaction.md` : repérage
  textuel pur, notion théorique pure, ou combinaison des deux. Le sujet
  mélange les trois familles sans qu'aucune ne domine entièrement, la part
  de repérage textuel pur étant prépondérante aux difficultés basses.

Distribution cible du nombre de propositions vraies, pour 15 questions :

| Propositions vraies | Nombre de questions |
|---|---|
| 1 (QRU) | 4 à 5 |
| 2 | 4 |
| 3 | 3 à 4 |
| 4 | 1 à 2 |
| 5 | 0 à 1 |

Pour 13 questions, conserver les mêmes proportions.

#### Justification et notions de chaque proposition

Chaque proposition, vraie comme fausse, comporte une `justification` et, le
cas échéant, un tableau `notions`.

1. La `justification` commence par la citation qui permet de trancher,
   littérale, dans la langue de l'article, sans traduction ni altération :
   « citation » (localisation). Une citation est une seule phrase, ou une
   seule donnée de tableau, ou la référence d'une figure, jamais un
   paragraphe ; une phrase longue est abrégée par […]. La localisation
   précise la section et, selon le cas, le tableau ou la figure.
   Elle se poursuit par l'explication, en français, en une à trois phrases.
2. Cas sans citation possible : proposition portant sur une information
   absente de l'article, commencer par « Absence de mention » en indiquant les
   sections vérifiées ; proposition de notion théorique indépendante du texte,
   commencer par « Sans objet ».
3. Toute proposition qui mobilise une notion théorique renseigne `notions`
   avec les entrées du référentiel (`id`, `numero`, `role`) : `evaluee` pour
   la notion testée, `associee` pour un prérequis ou une notion dépendante
   convoquée par la proposition. Plusieurs notions sont admises. Une
   proposition de pur repérage dans le texte peut avoir `notions` vide.
4. Dans l'explication, placer le `numero` entre parenthèses juste après la
   notion nommée, par exemple (036) ou (036, 037). Les numéros cités dans la
   justification et ceux du champ `notions` sont identiques.

Exemple (article fictif) : « Specificity decreased with age (P < .001) »
(Results, Diagnostic performance). La spécificité du test diminue quand l'âge
augmente ; la proposition inverse le sens de l'association (073).

### Étape 4. Contrôler la qualité

Vérifier chaque point avant de produire la sortie, et refuser de conclure tant
qu'un point échoue :

1. Chaque proposition est ancrée dans le texte : la justification débute par
   la citation littérale (une phrase ou une donnée) et sa localisation, puis
   l'explication.
2. Aucune question ne dépend d'une connaissance clinique externe à l'article,
   sauf notion de méthodologie explicitement au programme, en épidémiologie ou en statistique notamment.
3. La distribution des propositions vraies est conforme au tableau ci-dessus.
4. Les propositions vraies ne sont pas systématiquement plus longues ou plus
   nuancées que les fausses.
5. Aucune formulation absolue non justifiée (toujours, jamais, exclusivement)
   servant d'indice de fausseté.
6. Aucune redondance : deux questions ne portent pas sur la même notion sous
   un habillage différent.
7. La difficulté moyenne observée correspond à `difficulte_cible` à plus ou
   moins 1.
8. Les objectifs pédagogiques demandés sont tous couverts par au moins une
   question.
9. Chaque énoncé suit le gabarit fixe de la section 1 de
   `references/regles-redaction.md`, sans négation, sans abréviation, sans
   mélange de thèmes. Aucune proposition ne comporte de double négation.
10. Les trois familles de questions (repérage textuel, notion théorique,
    combinaison) sont représentées, dans les proportions attendues au niveau
    de `difficulte_cible` (`references/regles-redaction.md`, section 2).
11. Chaque citation est retrouvée mot pour mot dans l'article (seules les
    coupures de fin de ligne et les abrègements par […] sont tolérés), tient
    en une phrase ou une donnée, et porte une localisation exacte.
12. Toute proposition qui mobilise une notion théorique renseigne `notions`.
    Chaque `id` et `numero` existe dans le référentiel et correspond à la
    même entrée ; les numéros entre parenthèses de la justification sont ceux
    du champ `notions`. Aucune notion n'est inventée ni rattachée par
    approximation lointaine : à défaut, `notions` reste vide et la limite est
    consignée dans `controle_qualite.reserves`.
13. Les notions demandées par l'utilisateur sont rattachées à des
    propositions dont `notions` les mentionne.

### Étape 5. Produire la sortie

Émettre un objet JSON unique conforme à `assets/schema-sujet-lca.json`, sans
texte avant ni après, dans un bloc de code `json`. La fiche de l'étape 1 est
restituée dans `fiche_article`, première clé de l'objet, et la version du
référentiel dans `sujet.referentiel_notions`. Si l'utilisateur demande en
outre une version lisible, la fournir après le JSON.

## Propriété intellectuelle

Ne pas reproduire de passages étendus de l'article. Les énoncés, les
propositions et les explications reformulent le contenu. La seule
reproduction littérale admise est la citation de justification : une phrase
ou une donnée par proposition, jamais un paragraphe. Ne jamais joindre le
texte intégral de l'article dans la sortie.

## Fichiers de référence

- `references/regles-redaction.md` : règles d'écriture des questions de LCA.
  À lire à l'étape 3, systématiquement.
- `references/grilles-par-type-etude.md` : notions évaluables par type
  d'étude. À lire à l'étape 2, section correspondant au type identifié.
- `references/calibration-difficulte.md` : opérationnalisation de l'échelle
  de difficulté de 1 à 10. À lire lorsque `difficulte_cible` est fournie ou
  lorsque le contrôle qualité du point 7 échoue.
- `assets/schema-sujet-lca.json` : schéma de la sortie. À lire à l'étape 5.
- `assets/boussole_lca_notions.json` : référentiel figé de 143 notions, en
  lecture seule. À consulter aux étapes 2 et 3 selon la section « Référentiel
  de notions ».
