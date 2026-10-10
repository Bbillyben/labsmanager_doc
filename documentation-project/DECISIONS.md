# Décisions durables

## DOC-001 — Priorité des publics

Ordre de développement : 1. utilisateurs ; 2. administrateurs ; 3. développeurs.

## DOC-002 — Documentation utilisateur orientée parcours

Organiser d'abord la documentation utilisateur autour des tâches, besoins et parcours métier, et non de l'arborescence du code, des modèles Django ou d'une copie mécanique du menu.

## DOC-003 — Documentation language

English is the primary documentation language. Design the documentation for multilingual content from the start; French is the first additional language.

## DOC-004 — Primary user audiences

The first user documentation targets laboratory users and project leaders. Explain permission-dependent differences where relevant instead of duplicating sections by role.

## DOC-005 — Version target

The documentation targets LabsManager v1.0. Its React interface is the reference user interface. Document legacy Django screens only where a function still genuinely requires them.

## DOC-006 — Historical documentation reuse

Existing pages, links and assets may be reused when relevant. There is no specific compatibility policy for historical URLs at this stage; reorganisation is allowed when it improves the documentation.

## DOC-007 — Mémoire hors publication

`documentation-project/` est la mémoire du chantier ; ses fichiers ne sont pas ajoutés à la navigation utilisateur publiée.

## DOC-008 — Captures sans données réelles

Les captures de documentation utilisent exclusivement des données de démonstration ou non sensibles.

## DOC-009 — Localisation MkDocs

Conserver la configuration MkDocs/Material et les chemins anglais existants. Utiliser `mkdocs-static-i18n` avec l'anglais à la racine, les traductions françaises suffixées `.fr.md`, et le repli anglais pour les pages non encore traduites.

## DOC-010 — Screenshot request contract

Les captures documentaires sont demandées depuis ce dépôt au moyen de `documentation-project/screenshot-request.json` (contrat JSON v1). Le moteur Playwright externe lit la demande, écrit les PNG sous `docs/assets/screenshots/` et son résultat dans `documentation-project/screenshot-result.json`. Codex ne considère une capture disponible que si le résultat du batch correspondant indique `success` et si le PNG existe. La demande décrit l'intention fonctionnelle ; les sélecteurs et interactions navigateur restent dans l'outil Playwright.

## DOC-011 — Catalogue sémantique de scénarios de capture

Codex Documentation exprime les besoins de capture via un catalogue borné de scénarios fonctionnels et de paramètres explicites dans le contrat JSON v1. Les détails de navigation et de Playwright restent dans Codex Capture. Les anciens scénarios peuvent rester des alias de compatibilité. Une intervention de Codex Capture est normalement nécessaire pour une nouvelle famille fonctionnelle ou une rupture de l’interface, pas pour chaque nouveau lot documentaire. Les valeurs proposées, leurs conditions de validation et les besoins futurs sont décrits dans `SCREENSHOT_SCENARIO_REQUIREMENTS.md`.

## DOC-012 — Tâches et jalons réunis dans le guide Projects

La documentation utilisateur Projects traite tâches et jalons dans une même page : l’interface React les présente dans la rubrique « Milestones and tasks » et permet de les distinguer par filtre. Les deux vues peuvent recevoir des captures distinctes lorsque cela facilite la lecture. La finance liée au projet reste dans un lot documentaire ultérieur.

## DOC-013 — Finance suit les vues React du projet et l’explorateur distinct

La documentation Finance décrit les fonds dans la rubrique Funds du projet, les budgets et contributions dans leurs rubriques propres et l’explorateur comme liste transversale de lignes de financement. Elle n’introduit pas de fiche de fonds ni de courbe financière autonome que l’interface React Finance n’expose pas. Le widget d’évolution des dépenses appartient au futur lot Dashboards.
