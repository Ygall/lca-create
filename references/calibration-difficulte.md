# Calibration de la difficulté

La difficulté d'une question tient à trois déterminants : la profondeur du
traitement cognitif exigé, la distance entre l'information et sa formulation
dans l'article, et la proximité des propositions fausses avec la réponse
exacte. Une question n'est pas rendue difficile en multipliant les
propositions vraies ni en obscurcissant l'énoncé.

## Niveaux

| Niveau | Traitement cognitif | Localisation de l'information | Distracteurs |
|---|---|---|---|
| 1 à 2 | Identification | Explicite, énoncée telle quelle | Grossièrement faux |
| 3 à 4 | Compréhension | Explicite, reformulée | Plausibles mais franchement discriminables |
| 5 à 6 | Application | Dispersée sur deux sections, calcul simple | Erreurs classiques de raisonnement |
| 7 à 8 | Analyse | Implicite, à reconstituer | Erreurs fines, nuances de formulation |
| 9 à 10 | Évaluation critique | Non énoncée, repose sur une absence ou une incohérence | Très proches de la réponse exacte |

## Correspondance avec les notions

- Niveaux 1 à 2 : type d'étude, objectif principal, population incluse,
  identification du critère de jugement principal.
- Niveaux 3 à 4 : lecture du diagramme de flux, distinction critère principal
  et secondaire, identification du comparateur, lecture directe d'un tableau.
- Niveaux 5 à 6 : calcul et interprétation d'une réduction absolue du risque,
  du nombre de sujets à traiter, lecture d'un intervalle de confiance,
  cohérence entre test statistique et nature des variables.
- Niveaux 7 à 8 : identification d'un biais non déclaré, conséquence d'un
  écart entre population randomisée et population analysée, portée d'une
  analyse en sous-groupe non préspécifiée, interprétation d'une marge de
  non-infériorité.
- Niveaux 9 à 10 : repérage d'une incohérence entre méthodes et résultats,
  d'une sur-interprétation causale de la discussion, d'un critère composite
  dont l'effet repose sur sa composante la moins pertinente, d'une multiplicité
  non contrôlée invalidant une conclusion secondaire.

## Composition d'un sujet

`difficulte_cible` fixe la moyenne, non l'uniformité. Un sujet reste
discriminant lorsqu'il comporte un gradient. Répartition indicative pour une
cible donnée D :

- 20 % des questions à D moins 2,
- 60 % des questions à D plus ou moins 1,
- 20 % des questions à D plus 2.

Borner les valeurs à l'intervalle 1 à 10. Pour D inférieure ou égale à 3,
supprimer la strate basse ; pour D supérieure ou égale à 8, supprimer la
strate haute.

Renseigner la difficulté question par question dans la sortie, ce qui permet
la vérification du point 7 du contrôle qualité.
