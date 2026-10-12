# Backlog documentaire

`MATRIX.md` suit la couverture par parcours ; ce fichier décrit les lots restants.

## P0 — terminé

- Prise en main, navigation, recherche, fiche personne et fiche projet : pages et six captures validées pour ce périmètre.

## P1 People — terminé

- Aperçu de la personne, projets et contrats, absences : pages relues et validées.
- Les trois captures du batch `P1-people-001` sont intégrées après vérification du résultat et contrôle visuel.

## Infrastructure documentaire — catalogue Projects disponible

- Les primitives `project-section` (overview/participants), `project-planning` (tasks/milestones) et `calendar` (project/month) sont confirmées avec `employee` sur ORION ; `P1-projects-001` les utilise directement.
- Les autres familles et valeurs de `SCREENSHOT_SCENARIO_REQUIREMENTS.md` restent à confirmer ou à implémenter au rythme des lots futurs. Aucune intervention Codex Capture n’est requise pour ce batch.

## P1 Projects — terminé pour les parcours de consultation retenus

- Aperçu, participants, tâches et jalons, calendrier mensuel : pages validées et quatre captures du batch `P1-projects-001` intégrées après contrôle visuel.
- Restent pour des lots ultérieurs : état overdue sur SELENE/LYRA, création/modification et vues de planning avancées. Le financement lié au projet est couvert par P1 Finance.

## P1 Finance — terminé pour les parcours de consultation retenus

- Trois pages finalisées : fonds liés au projet, budgets et dépenses, Fund explorer.
- Les cinq captures `P1-finance-001` ont un résultat `success`, existent, ont été contrôlées visuellement et sont intégrées.
- Restent pour des lots ultérieurs : comparaisons de consommation P1-14/15 seulement si elles apportent une différence utile, widget Dashboard Expense evolution, procédures de modification, exports et rapports après vérification de leur périmètre.
- P1-16, courbe propre à un fonds, n’est pas une capture Finance nécessaire.

## P1 Dashboards — terminé pour les parcours retenus

- Deux pages utilisateur finalisées : lecture des tableaux personnels et personnalisation de base.
- Le batch corrigé `P1-dashboards-001` rapporte 3/3 `success`. Les trois captures Employee overview, Team overview et Laboratory overview ont passé le contrôle visuel et sont intégrées.
- La première utilisation et la personnalisation sont décrites sans capture dédiée. Expense evolution est préconfiguré sur le tableau d’un projet ; sa capture reste différée.

## P1 Calendars — terminé pour les parcours retenus

- Une page finalisée couvre les deux onglets du calendrier transversal React, les modes Calendar/Resources, les périodes, filtres, interactions et impression. Le calendrier propre à un projet reste documenté dans P1 Projects.
- `P1-calendars-001` rapporte 1/1 `success` ; P1-20 montre le General calendar mensuel attendu, a passé le contrôle visuel, est intégré dans la page et ajouté à `screenshot-refresh.json`.
- Les vues Resources et Gantt multi-projets sont décrites sans PNG dédié ; leurs états restent différés dans le catalogue Capture. Elles ne bloquent pas les parcours documentés.

## P1 Teams — terminé pour les parcours retenus

- Deux pages décrivent la liste, la fiche Team et la gestion de la composition selon les capacités React, sans reprendre les procédures People.
- `P1-teams-001` rapporte 2/2 `success`. P1-27 liste Teams et P1-28 fiche Information de Quantum Materials Studio ont été contrôlées visuellement, intégrées et ajoutées au manifeste permanent (24 images).
- La création et la modification sont décrites selon les droits, sans capture de formulaire dédiée.

## P1 Organizations — terminé pour les parcours retenus

- Une page commune couvre Institutions et Funders : mêmes listes/fiches React, recherche, tri, onglets, contacts, informations complémentaires et actions selon droits ; les relations aux fonds distinguent les deux types.
- `P1-organizations-001` rapporte 2/2 `success`. P1-29 liste Institutions avec NVAU et P1-30 fiche VRC Information ont été contrôlées visuellement, intégrées et ajoutées au manifeste permanent (26 images).
- Les listes et fiches Funders/Institutions non illustrées partagent l’interface ; aucune capture redondante ni contact démo non peuplé n’est requis.

## P1 Reports & Exports — terminé pour les parcours retenus

- Une page couvre les rapports Employee/Project et les exports de listes React. Le format Word/PDF se choisit dans le menu de la fiche ; le dialogue charge les modèles correspondants. Employee propose une période, Project non. Les listes proposent XLSX/CSV/TSV/XLS sans modèle de rapport.
- P1-24 (Camille ORREN, Word avec période) et P1-25 (ORION, PDF sans période), profil `labmanager`, utilisent `entity-report`. Capture a validé les deux dialogues avec modèles démo sélectionnés et bouton Export actif.
- `P1-reports-001` rapporte 2/2 `success`. Les deux dialogues ont été contrôlés visuellement et intégrés ; P1-24/25 figurent dans le manifeste permanent, désormais à 28 captures.

## P1 Settings & Preferences — terminé pour les parcours retenus

- Une page couvre les cinq sections personnelles React : User settings, Interface, Notifications, Favorites and subscriptions (Common) et Stale alerts. Les listes de référence et `admin/*` sont hors lot. Les préférences sont propres à l’utilisateur ; les switches et choix s’enregistrent au changement, les nombres/textes au blur ou avec Entrée, le mot de passe via Save.
- P1-31/32/33 retiennent User, Interface et Notifications avec le profil normal `employee`. Common et Stale sont couverts sans image dédiée. Le choix Calendar/List des notifications règle le courriel d’absences ; les horizons Stale règlent des synthèses Dashboard, sans préférence pour le mode du calendrier global.
- `P1-settings-001` rapporte 3/3 `success`. User, Interface et Notifications ont été contrôlés visuellement, intégrés et ajoutés au manifeste permanent, qui contient désormais 31 captures. Common et Stale restent documentés sans image dédiée.

## P1 Tools — terminé pour les parcours retenus

- Une page compacte couvre les sept entrées du menu Tools React : Data consistency, Import, Organization chart, Contracts, Fund explorer, Budget explorer et Expenses. Les usages financiers déjà documentés renvoient à P1 Finance.
- Trois images nouvelles sont retenues : organigramme peuplé, liste transversale Contracts et entrée Import avec type Employees sélectionné. Fund explorer dispose déjà de P1-13 ; les autres listes et Data consistency n’ajoutent pas de repère visuel indispensable.
- Le résultat `P1-tools-001` rapporte 2/3 `success` : Contract Hub (P1-35) et Import Employees (P1-36), contrôlés visuellement et intégrés. Le manifeste permanent contenait alors 33 captures. `labmanager` ne peut pas ouvrir Import ; la capture intégrée utilise `admin`.
- La reprise ciblée `P1-tools-organization-chart-001` avec `labmanager` / Noé rapporte 1/1 `success`. P1-34 montre plusieurs dizaines de nœuds Employee et leurs relations, sans chargement ni panneau parasite ; le PNG a passé le contrôle visuel, est intégré et ajouté au manifeste permanent (34 captures). Le précédent PNG `employee` à un seul nœud n’a jamais été intégré. P1-35/36 restent les captures validées du premier batch, sans recapture.

## Autres domaines P1 — lots ultérieurs
- Contrats et absences : procédures de modification selon droits ; impression et exports avancés hors des parcours documentés ici.

## P2 — fonctionnalités avancées

- Recherche avancée, personnalisation avancée des tableaux de bord, Gantt et dépendances après vérification. Les outils transversaux et imports React courants sont couverts par P1 Tools.

## P3 — référence et usages occasionnels

- Glossaire, variantes de configuration, filtres, formats et rapports historiques après vérification. Les réglages personnels et notifications React courants sont couverts en P1 Settings & Preferences.

## Admin — Installation & initial setup — terminé

- Quatre pages distinctes du guide utilisateur couvrent l’architecture actuelle, Docker Compose, le déploiement bare metal et l’initialisation commune. L’ancienne page Installation pointe vers ce nouveau bloc ; ses instructions obsolètes ne restent plus dans la navigation.
- `invoke install` est la procédure canonique : migrations, contrôles, collectstatic, puis `group-fixture` et `initial-report-data`. `invoke install --super-user` et `invoke superuser` sont confirmés par l’aide Invoke.
- Le générateur `generate_demo_data` est documenté seulement pour une base dédiée de démonstration/test, avec ses protections et le risque de `--reset`. Aucune capture n’est demandée ; le manifeste permanent reste à 34 images.
- Builds MkDocs EN et FR/fallback réussis ; liens internes des quatre pages Admin et du renvoi historique vérifiés. Aucun déploiement destructif n’a été exécuté pour ce lot.

## Admin — Instance administration — terminé pour les parcours retenus

- Trois pages couvrent les quatre sections React Settings Administration, les neuf listes du registre actuel et Data consistency. Les comptes/groupes existants relèvent de Django Admin seulement pour les opérations absentes de React.
- Deux captures sont retenues : General Settings (`admin`) et le groupe Fund des listes (`admin`). Data consistency est expliqué sans capture dédiée tant qu’un exemple non vide et stable n’est pas confirmé.
- `ADMIN-instance-001` rapporte 2/2 `success`. ADM-01 General et ADM-02 Fund ont été contrôlées visuellement, intégrées aux pages et ajoutées au manifeste permanent (36 images). Builds MkDocs EN et FR/fallback, liens et images vérifiés.

## Developer — Plugin development — terminé

- Quatre pages développeur couvrent découverte/activation, structure et exemple minimal, routes/permissions, extensions Dashboard/Search/Calendar et tests/débogage. Les quatre anciennes pages plugin pointent vers ce guide et ne répètent plus les anciennes API.
- Aucun nouveau scénario ni PNG : le registre `SCREENSHOTS.md` et le manifeste permanent restent inchangés (36 captures). Builds EN/FR et liens internes vérifiés.

## Traduction française — guide utilisateur — terminé

- Les 23 pages publiées du guide utilisateur et la page d’accueil ont une version `.fr.md` complète. Les libellés d’interface affichés en anglais restent en anglais ; les explications, liens et textes alternatifs sont en français.
- À chaque évolution ultérieure d’une page utilisateur anglaise, mettre à jour sa paire française dans le même lot et vérifier les deux builds. Admin, Developer et legacy sont hors de ce lot.
