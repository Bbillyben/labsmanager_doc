# État du chantier — 11 octobre 2026

**Phase :** P0, P1 People, P1 Projects, P1 Finance, P1 Dashboards, P1 Calendars, P1 Teams, P1 Organizations, P1 Reports & Exports, P1 Settings & Preferences et P1 Tools terminés pour les parcours retenus. Admin — Installation & initial setup terminé. Cible : LabsManager v1.0 React.

**Audit Dashboards :** les comptes synthétiques `employee`, `leader` et `labmanager` ont chacun un tableau personnel préconfiguré. React propose aussi un choix explicite du modèle lors de la première création, un sélecteur de tableaux et la personnalisation (widgets, disposition sur grand écran, tableau par défaut). `Expense evolution` est préconfiguré dans le tableau d’un projet, pas dans les trois modèles personnels. Deux pages utilisateur sont finalisées ; les trois captures personnelles sont intégrées.

**Captures :** request et result `P1-settings-001` concordent (3/3 `success`). Le précédent batch `P1-reports-001` concordait (2/2 `success`). P1-20 montre le General calendar mensuel avec filtre et absence visibles, sans chargement ni panneau parasite ; il est intégré. `screenshot-refresh.json` contient désormais les 31 captures intégrées. P1-21/22 restent différées faute de mode Capture confirmé pour le Gantt multi-projets et Resources.

**Vérification :** build MkDocs EN et FR/fallback réussi ; liens et trois images Dashboard valides dans les deux locales. Les messages de liens préexistants concernent des pages hors lot.

**Vérification Calendars :** le résultat et le PNG `P1-calendars-001` ont été contrôlés. MkDocs EN et FR/fallback se construisent ; les liens et l’image de la page Calendars sont valides dans les deux locales.

**P1 Teams :** deux pages finalisées. La liste et la fiche Quantum Materials Studio du batch `P1-teams-001` ont un résultat `success`, existent, ont été contrôlées visuellement et sont intégrées. P1-27/28 figurent dans le manifeste permanent. Les parcours de consultation et de gestion selon les droits sont couverts. Build MkDocs EN et FR/fallback réussi ; liens et deux PNG Teams valides dans les deux locales.

**P1 Organizations :** une page commune finalisée pour Institutions/Funders. `P1-organizations-001` rapporte 2/2 `success` ; la liste NVAU et la fiche VRC Information ont été contrôlées visuellement, intégrées et ajoutées au manifeste permanent (P1-29/30). Les parcours de consultation et les actions selon les droits sont couverts. Build MkDocs EN et FR/fallback réussi ; liens et deux PNG Organizations valides dans les deux locales.

**P1 Reports & Exports :** page finalisée pour les rapports Employee/Project et les exports de listes. `P1-reports-001` rapporte 2/2 `success` ; Camille ORREN Word avec From/To et ORION PDF sans période montrent chacun un modèle sélectionné et le contrôle Export. Les deux PNG ont été contrôlés visuellement, intégrés et ajoutés au manifeste permanent (28 captures). Builds EN et FR/fallback ainsi que liens/images vérifiés.

**P1 Settings & Preferences :** une page finalisée couvre les cinq sections personnelles React. `P1-settings-001` rapporte 3/3 `success` ; User, Interface et Notifications ont été contrôlés visuellement, intégrés et ajoutés au manifeste permanent (31 captures). Common et Stale sont couverts en texte. Builds MkDocs EN et FR/fallback ainsi que liens/images vérifiés.

**P1 Tools — terminé :** la page couvre les sept outils React et renvoie au guide Fund explorer. P1-35 Contract Hub et P1-36 Import Employees restent intégrées depuis `P1-tools-001`. La reprise ciblée `P1-tools-organization-chart-001` avec `labmanager` / Noé rapporte 1/1 `success` ; P1-34 montre plusieurs dizaines de nœuds et leurs relations, sans loader ni panneau parasite. Les trois PNG Tools ont été contrôlés visuellement et sont intégrés ; le manifeste permanent compte 34 images.

**Admin — Installation & initial setup terminé :** quatre pages techniques finalisées pour Docker, bare metal et initialisation ; l’ancienne page Installation renvoie vers elles. La task `invoke install` et ses deux fixtures, la syntaxe `--super-user`, le générateur démo et les services/chemins actuels ont été vérifiés dans le dépôt. Builds MkDocs EN et FR/fallback réussis ; liens internes vérifiés. Aucune capture nouvelle ; manifeste à 34 images.

**Prochaine action :** lot Admin Installation clos. Les autres lots restent hors de cette passe.

**Admin — Instance administration terminé :** trois pages React finalisées. Quatre sections Administration réservées à `is_staff` ; neuf listes lisibles après connexion et modifiables selon permissions ; Data consistency documenté selon droits. `ADMIN-instance-001` rapporte 2/2 `success` ; ADM-01 General et ADM-02 Fund ont été contrôlées visuellement et intégrées. `screenshot-refresh.json` contient 36 captures intégrées. Builds EN et FR/fallback, liens et images vérifiés.

**Developer — Plugin development terminé :** quatre pages pratiques et quatre renvois historiques finalisés. Découverte, activation, mixins, URLs, droits, Dashboard, Search, Calendar, tests et limites React documentés sur le code courant. Aucune capture nouvelle ; manifeste permanent à 36 images. Builds MkDocs EN/FR et liens vérifiés.

**Traduction française du guide utilisateur — terminée :** les 23 pages utilisateur publiées et la page d’accueil ont une traduction `.fr.md` complète. Navigation française complétée ; parité des pages, liens, images et builds EN/FR vérifiée. Les 36 captures existantes sont réutilisées sans modification du manifeste. Admin, Developer et legacy restent hors du périmètre.
