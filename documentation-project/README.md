# Mémoire du chantier documentaire

Ce dossier de travail n'est pas publié et ne doit pas entrer dans la navigation MkDocs. Il sert à reprendre la refonte sans réauditer l'application.

- `AUDIT.md` : photographie initiale et proposition de structure (à conserver comme état daté).
- `APPLICATION_CONTEXT.md` : faits applicatifs utiles à la rédaction, à corriger seulement si l'application change durablement.
- `DECISIONS.md` : décisions durables, jamais un journal.
- `STATUS.md` : phase, progrès et questions à reprendre.
- `MATRIX.md` : couverture par parcours, source principale de suivi.
- `BACKLOG.md` : lots décidés et priorités ; ne recopie pas la matrice.
- `STYLE_GUIDE.md` : conventions éditoriales établies.
- `SCREENSHOTS.md` : registre humain et cahier des charges des captures.
- `SCREENSHOT_SCENARIO_REQUIREMENTS.md` : inventaire des besoins futurs et catalogue fonctionnel proposé pour Codex Capture.

Pour une passe normale, ouvrir seulement les fichiers utiles parmi `README.md`, `STATUS.md`, `DECISIONS.md`, la ligne pertinente de `MATRIX.md` et `APPLICATION_CONTEXT.md`. Un petit correctif peut se limiter à README, STATUS et une ligne de MATRIX. Lire `SCREENSHOTS.md` pour les images, `STYLE_GUIDE.md` pour la rédaction/relecture et `BACKLOG.md` pour planifier. Charger le minimum de contexte nécessaire à chaque tâche.

Sources : pages publiées de ce dépôt pour leur état actuel ; application LabsManager pour vérifier un comportement précis. Les documents historiques `labsmanager/docs/react-migration/` (dans le dépôt applicatif) sont des références secondaires, à consulter uniquement si cette mémoire ne suffit pas, jamais systématiquement. Inspecter le code seulement pour lever une incertitude ou confirmer l'état actuel.

Après chaque lot, mettre à jour STATUS si le chantier évolue, MATRIX si la couverture évolue, BACKLOG si les travaux changent, SCREENSHOTS si une capture change. Ajouter à DECISIONS ou STYLE_GUIDE seulement une décision durable ; modifier APPLICATION_CONTEXT seulement pour un changement applicatif durable. Git porte l'historique détaillé. Ne pas dupliquer les mêmes détails entre fichiers.

## Captures automatisées

`SCREENSHOTS.md` planifie les captures et leurs états. `screenshot-request.json` est la demande lisible par le moteur Playwright externe pour le lot courant ; celui-ci écrit les PNG sous `docs/assets/screenshots/` et produit `screenshot-result.json`. Avant d'intégrer une image, vérifier que le résultat appartient au batch demandé, que sa capture est `success` et que le PNG existe. Les deux fichiers JSON sont des échanges opérationnels, pas la mémoire historique détaillée du chantier.
