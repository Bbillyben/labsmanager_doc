# État du chantier — 7 octobre 2026

**Phase :** P0, P1 People, P1 Projects et P1 Finance terminés pour les parcours retenus ; **P1 Dashboards actif, préparation documentaire en cours**. Cible : LabsManager v1.0 React.

**Audit Dashboards :** les comptes synthétiques `employee`, `leader` et `labmanager` ont chacun un tableau personnel préconfiguré. React propose aussi un choix explicite du modèle lors de la première création, un sélecteur de tableaux et la personnalisation (widgets, disposition sur grand écran, tableau par défaut). `Expense evolution` est préconfiguré dans le tableau d’un projet, pas dans les trois modèles personnels. Deux pages utilisateur sont rédigées, sans image non produite.

**Captures :** P1-17 `dashboard(template=employee)` est disponible mais le batch reste différé. P1-18 `template=leader` et P1-19 `template=labmanager` ne sont pas confirmés dans le catalogue Capture ; ils requièrent une extension avec `profile=leader` et `profile=labmanager` respectivement. Aucun batch Dashboard ni PNG Dashboard n’est généré. `screenshot-request.json` et `screenshot-result.json` restent sur `P1-finance-001`.

**Vérification :** build MkDocs EN et FR/fallback réussi ; la rubrique Dashboards est présente dans les deux navigations. Les 32 pages du guide contrôlées dans les deux locales n’ont aucun lien local manquant. Seuls les messages historiques des anciennes pages subsistent.

**Prochaine action :** Codex Capture ajoute et valide les deux valeurs manquantes du scénario `dashboard`, puis Codex Documentation prépare le batch `P1-dashboards-001` avec les trois profils.
