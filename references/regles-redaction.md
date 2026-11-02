# Règles de rédaction des questions de LCA

> Ces règles s'appuient sur les principes usuels de rédaction d'un bon QRM/QRU et sur
> l'expérience de l'auteur en enseignement de la LCA. Ce fichier reste ouvert à un
> remplacement ou un complément par une grille institutionnelle propre à l'utilisateur.

## Table des matières

1. Formule de l'énoncé
2. Typologie des questions
3. Propositions
4. Ancrage dans le texte
5. Justifications
6. Anti-patrons à proscrire
7. Exemples

## 1. Formule de l'énoncé

Chaque énoncé suit un gabarit fixe, invariant d'un sujet à l'autre :

> N) Concernant [thème], quelle(s) est (sont) la (les) proposition(s) exacte(s) ?

- [thème] désigne un point précis de l'article (un paragraphe, une section, une donnée
  particulière), jamais une juxtaposition de plusieurs points.
- L'énoncé est toujours de forme interrogative ou affirmative, jamais négative. Ne pas
  écrire « quelle(s) proposition(s) n'est (ne sont) pas exacte(s) » : si une exception doit
  être interrogée, resserrer le thème plutôt que nier l'énoncé.
- Ne pas utiliser d'abréviation dans l'énoncé, y compris un sigle déjà défini dans
  l'article (le développer ou le réintroduire).
- Pas de majuscule ailleurs qu'en début de phrase, pas de ponctuation superflue.

## 2. Typologie des questions

Un sujet mélange trois familles de questions, sans qu'une famille domine l'ensemble :

1. **Repérage textuel pur** : la réponse se lit directement dans l'article, sans mobiliser
   de notion méthodologique au-delà de la compréhension du texte (par exemple : l'âge
   médian des participants, le nombre de centres, la méthode de calcul d'un intervalle de
   confiance telle que rapportée).
2. **Notion théorique pure** : la réponse mobilise une connaissance méthodologique
   générale, vraie indépendamment de l'article (par exemple : ce que mesure un nombre de
   sujets à traiter, la définition d'un biais de Berkson, la différence entre risque relatif
   et odds ratio).
3. **Combinaison** : une donnée du texte doit être interprétée à la lumière d'une notion
   théorique, dans un sens ou dans l'autre — reconnaître dans le texte l'application d'une
   notion (par exemple : repérer que l'étude présente comme significative une différence
   qu'elle n'a pas testée statistiquement), ou appliquer une notion à une donnée chiffrée du
   texte (par exemple : déduire d'un intervalle de confiance rapporté si un résultat est
   compatible avec une absence d'effet).

Chaque question est rattachée principalement à une seule de ces trois familles ; il est possible de 
mobiliser deux familles si cela a un lien logique avec le [thème] de la question.

Toute proposition qui mobilise une notion théorique (familles 2 et 3) la référence dans le
référentiel `assets/boussole_lca_notions.json` (voir section 5 et SKILL.md, « Référentiel
de notions »). Une proposition de pur repérage dans le texte n'a pas à le faire.

Pour `difficulte_cible` inférieure ou égale à 3, la famille 1 domine largement le sujet ;
la part des familles 2 et 3 croît avec la difficulté cible (voir
`references/calibration-difficulte.md`).

## 3. Propositions

- Cinq propositions par question, notées A à E (a à e à l'écrit).
- Au moins une proposition vraie ; le nombre de vraies varie selon la distribution cible
  fixée dans SKILL.md.
- Propositions homogènes en longueur, en registre et en structure grammaticale. La
  formulation d'une proposition ne doit jamais, à elle seule, trahir si elle est vraie ou
  fausse.
- Pas de majuscule en début de proposition, pas de ponctuation finale, pas d'abréviation.
- Une proposition isolée peut être formulée négativement (par exemple : « n'a pas été
  préspécifiée »), mais jamais avec une double négation. Une proposition dont la lecture
  exige de lever deux négations est invalide et doit être reformulée.
- Ne jamais utiliser de proposition du type « toutes les propositions précédentes sont
  exactes / fausses ».
- Ne pas utiliser de jugement de valeur ni de terme sujet à discussion (« efficace »,
  « adapté », « suffisant » employés sans critère explicite) : remplacer par une
  formulation objective et vérifiable.
- Les distracteurs doivent être plausibles : une proposition fausse à l'évidence, sans lien
  avec le contenu ou le vocabulaire de l'article, n'est pas un distracteur valide.
- Les propositions fausses reposent sur des erreurs plausibles et identifiables : confusion
  entre risque relatif et réduction absolue, confusion entre association et causalité,
  extrapolation hors population d'étude, interprétation d'un résultat non significatif
  comme preuve d'absence d'effet, lecture erronée d'un intervalle de confiance, confusion
  entre critère principal et secondaire, confusion entre analyse en intention de traiter et
  per-protocole.
- Ne pas construire une proposition fausse par pure invention numérique sans lien avec les
  valeurs du texte : la valeur erronée doit correspondre à une erreur de raisonnement
  identifiable, pas à un chiffre arbitraire.

## 4. Ancrage dans le texte

- Toute proposition doit être décidable à partir de l'article seul, complété des seules
  connaissances méthodologiques attendues d'un étudiant de DFASM.
- Les questions portant sur des données absentes de l'article sont admises uniquement
  lorsqu'elles évaluent le repérage d'une information manquante (par exemple : absence de
  calcul du nombre de sujets nécessaires, absence de déclaration de conflits d'intérêts).
  L'énoncé doit alors rendre explicite que l'on interroge la présence ou l'absence de
  l'information.
- Répartir les questions sur l'ensemble de l'article, dans son ordre de lecture :
  justification et objectif de l'étude, type d'étude et schéma, population et critères
  d'inclusion/exclusion, méthodes de mesure et d'analyse, résultats descriptifs, résultats
  principaux, analyses complémentaires, discussion, forces et limites, implications.

## 5. Justifications

- Une justification par proposition, vraie comme fausse. Elle suit toujours le même ordre :
  la citation, puis l'explication.
- Citation : « texte » (localisation), littérale, dans la langue de l'article, sans
  traduction ni altération. C'est la phrase, la donnée de tableau ou la référence de figure
  qui permet de trancher, rien de plus ; une phrase longue est abrégée par […]. La
  localisation donne la section et, le cas échéant, le tableau ou la figure. Pour une
  proposition fausse, citer le passage qui établit la vérité contredite par la proposition.
- Explication : en français, une à trois phrases. Elle reformule ; ne pas reproduire de
  passage étendu.
- Pour les propositions fausses, nommer l'erreur de raisonnement visée (champ
  `erreur_visee`), ce qui permet la réutilisation pédagogique du corrigé.
- Notions : lorsqu'une notion théorique est mobilisée, placer son numéro entre parenthèses
  dans l'explication, juste après la notion nommée, par exemple (036) ou (036, 037), et
  renseigner `notions` avec les mêmes numéros. Une proposition peut référencer plusieurs
  notions, notamment une notion et son prérequis lorsqu'elle les associe (`role` :
  `evaluee` ou `associee`). Ne jamais attribuer un numéro sans l'avoir lu dans le
  référentiel.
- Sans citation possible : « Absence de mention » suivi des sections vérifiées, pour une
  information absente de l'article ; « Sans objet » pour une proposition de notion
  théorique indépendante du texte.

## 6. Anti-patrons à proscrire

- Questions de pure connaissance clinique sans lien avec l'analyse critique de l'article.
- Énoncé ou proposition mélangeant plusieurs thèmes (voir section 2).
- Proposition à double négation.
- Propositions comportant « toujours », « jamais », « exclusivement » lorsque ces termes
  servent uniquement d'indice de fausseté.
- Propositions du type « toutes les propositions précédentes sont exactes ».
- Jugement de valeur ou terme sujet à discussion, dans l'énoncé comme dans les
  propositions.
- Indices croisés : une question dont l'énoncé donne la réponse d'une autre.
- Questions dont la réponse dépend d'une convention statistique non consensuelle.
- Séries où la position des propositions vraies est régulière.
- Citation reformulée, tronquée sans […], traduite, ou ne figurant pas dans l'article.
- Citation de plus d'une phrase ou d'une donnée.
- Proposition à notion théorique sans numéro de notion, ou numéro absent du référentiel ou
  discordant entre la justification et le champ `notions`.

## 7. Exemples

**Exemple 1, notion : critère de jugement principal, difficulté 3, famille repérage textuel**

Énoncé : 6) Concernant les critères de jugement de cette étude, quelle(s) est (sont) la
(les) proposition(s) exacte(s) ?

Structure attendue : deux propositions vraies portant sur la nature composite du critère et
sur son délai de mesure, telles qu'énoncées dans l'article ; trois propositions fausses
portant respectivement sur un critère secondaire présenté comme principal, sur une mesure
non réalisée, et sur un délai erroné.

**Exemple 2, notion : interprétation d'un intervalle de confiance, difficulté 7, famille
combinaison**

Énoncé : 11) Concernant la spécificité et l'âge des participants, quelle(s) est (sont) la
(les) proposition(s) exacte(s) ?

Structure attendue : une seule proposition vraie (QRU) reliant le sens de la corrélation
rapportée dans le texte à sa traduction correcte en termes de performance du test ;
propositions fausses construites sur l'inversion du sens de la corrélation, sur
l'assimilation d'une corrélation à une causalité, et sur une confusion entre spécificité et
sensibilité.

**Exemple 3, illustration des trois familles, à propos d'une étude cas-témoins**

- Repérage textuel pur : « Concernant les témoins, quelle(s) est (sont) la (les)
  proposition(s) exacte(s) ? » avec une proposition portant sur le nombre de témoins
  appariés à chaque cas, tel qu'énoncé dans le texte.
- Notion théorique pure : « Concernant les biais possibles de cette étude, quelle(s) est
  (sont) la (les) proposition(s) exacte(s) ? » avec une proposition définissant un biais de
  Berkson en des termes généraux, vraie indépendamment de l'étude décrite.
- Combinaison : la même question, avec une proposition affirmant que le recours à des cas
  hospitaliers opérés expose à un biais de Berkson non discuté par les auteurs — ce qui
  exige de relier la définition théorique du biais à une caractéristique du recrutement
  décrite dans l'article.

**Exemple 4, justification d'une proposition fausse (article fictif)**

Proposition : « la sensibilité du test est supérieure chez les sujets de moins de 50 ans ».

Justification : « Sensitivity was 62.5% (25/40) in participants younger than 50 years and
85.0% (51/60) in those aged 50 years or older » (Results, Table 2). La sensibilité est plus
faible chez les moins de 50 ans : la proposition inverse le sens de la différence, et ces
résultats rapportent des sensibilités (073) sans comparaison testée entre les groupes.

`notions` : `[{"id": "sensibilite-specificite", "numero": "073", "role": "evaluee"}]`,
`erreur_visee` : inversion du sens d'une comparaison de sensibilités.

Un exemple de forme, pas de contenu : les numéros de notion sont toujours à relire dans le
référentiel de la version utilisée.
