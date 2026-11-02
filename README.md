# lca-create

Skill Claude qui génère un sujet d'entraînement de lecture critique d'article (LCA) au format des EDN, pour des étudiants en médecine de DFASM, à partir d'un article scientifique (PDF, PMID ou DOI).

La sortie est un JSON structuré (QRU et QRM à cinq propositions, 13 à 15 questions) conforme à `assets/schema-sujet-lca.json`. Chaque proposition est justifiée par une citation littérale de l'article, puis une explication, et peut renvoyer à une notion du référentiel Boussole LCA.

## Paramètres

- difficulté cible de 1 à 10 (défaut 5) ;
- objectifs pédagogiques en texte libre, ou notions du référentiel désignées par leur numéro, leur identifiant ou leur libellé ;
- nombre de questions, de 13 à 15.

## Contenu

| Fichier | Rôle |
|---|---|
| `SKILL.md` | Procédure en cinq étapes et contraintes. |
| `references/regles-redaction.md` | Règles d'écriture des questions et des justifications. |
| `references/grilles-par-type-etude.md` | Notions évaluables par type d'étude. |
| `references/calibration-difficulte.md` | Échelle de difficulté de 1 à 10. |
| `assets/schema-sujet-lca.json` | Schéma JSON de la sortie. |
| `assets/boussole_lca_notions.json` | Référentiel figé de 143 notions (Boussole LCA). Lecture seule. |

## Installation

Claude Code : copier le dossier dans `~/.claude/skills/lca-create/` (personnel) ou `.claude/skills/lca-create/` (projet).

claude.ai : téléverser le fichier `lca-create.skill` d'une release dans Paramètres, Capacités, Skills.

## Limites

- Le texte intégral de l'article est nécessaire : un PMID ou un DOI sans texte intégral accessible ne produit pas de sujet.
- Les questions générées doivent être relues par un enseignant avant usage.
- Le référentiel de notions est une proposition pédagogique, pas le programme officiel de LCA.

## Auteur et citation

Yves Gallien, CHU de Rennes et Université de Rennes. Voir `CITATION.cff`.

## Licence

À définir avant la publication publique.
