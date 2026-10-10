# Matrice de couverture

Mise à jour du 7 octobre 2026. Chaque ligne décrit un parcours, pas un écran ou un modèle. P0 et P1 People sont validés. P1 Projects est validé pour la consultation de l’aperçu, des participants, des tâches/jalons et du calendrier mensuel : les quatre PNG du batch `P1-projects-001` ont été contrôlés et intégrés. P1 Finance est validé pour la consultation : cinq captures du batch `P1-finance-001` ont été contrôlées et intégrées. Les comparaisons de consommation restent conditionnelles et la courbe de dépenses appartient au futur lot Dashboards. P1 Dashboards est audité et rédigé, mais les captures Leader et Lab manager attendent deux valeurs du scénario `dashboard` ; aucune fonction Dashboard n’est encore validée. Les autres domaines P1 ainsi que P2–P3 ne sont pas commencés.

| Domaine | Parcours / tâche | Page prévue | Priorité | État | Capture / illustration | Remarques |
|---|---|---|---|---|---|---|
| Prise en main | Accéder à LabsManager et comprendre l'accueil | `user-guide/getting-started/index.md` | P0 | Validé | P0-01 intégrée | Connexion dépendante du déploiement, décrite sans procédure spécifique |
| Navigation | Passer des rubriques aux fiches et reconnaître les actions permises | `user-guide/getting-started/interface.md` | P0 | Validé | P0-02 intégrée | Capacités contextuelles |
| Home | Reprendre une destination récente | `user-guide/getting-started/index.md` | P0 | Validé | P0-01 intégrée | Récents visibles sur l’accueil de démonstration |
| Recherche globale | Retrouver une personne, un projet ou un financement | `user-guide/finding-information/search.md` | P0 | Validé | P0-03/04 intégrées | Résultats et libellés vérifiés sur ORION ; visibilité selon droits |
| Listes et filtres | Filtrer, trier et ouvrir un résultat | `user-guide/finding-information/search.md` | P0 | Validé | Liste personne | Filtres selon la liste |
| Employés | Consulter identité, statut et hiérarchie | `user-guide/people/view-person.md` | P0 | Validé | P0-05 intégrée | Aperçu et navigation vérifiés sur Camille ORREN |
| Employés | Lire projets, contrats, absences et financement liés | `user-guide/people/view-person.md` | P0 | Validé | Fiche personne | Relations visibles ≠ accès autonome |
| Projets | Ouvrir une fiche et comprendre ses rubriques | `user-guide/projects/view-project.md` | P0 | Validé | P0-06 intégrée | Aperçu vérifié sur ORION |
| Employés | Voir projets et participations d'une personne | `user-guide/people/work-and-contracts.md` | P1 | Validé | P1-02 intégrée | Participation ORION, rôle, période, quotité et état vérifiés ; lien selon visibilité |
| Employés | Lire les informations complémentaires | `user-guide/people/view-person.md` | P1 | Validé | Aperçu P0 existant ; aucune nouvelle capture | React confirmé ; ajout/modification selon droits ; Camille sans valeur renseignée |
| Projets | Créer ou modifier un projet si autorisé | Consulter un projet | P1 | À analyser | Fiche Project | Vérifier capacités par contexte |
| Participants | Lire les rôles, périodes et quotités sur un projet | `user-guide/projects/people-and-responsibilities.md` | P1 | Validé | P1-05 intégrée | Bloc Participants sur Overview ; noms, rôles, quotités et périodes vérifiés |
| Tâches et jalons | Lire échéances, états et détails | `user-guide/projects/tasks-and-milestones.md` | P1 | Validé | P1-06/06b intégrées | Vues Task et Milestone distinctes et filtrées ; états, échéances et responsables vérifiés |
| Tâches et jalons | Créer ou modifier selon droits | Suivre tâches et jalons | P1 | À analyser | Feuille de détail | Capacités variables |
| Calendrier Project | Consulter les événements d’un projet en vue mensuelle | `user-guide/projects/project-calendar.md` | P1 | Validé | P1-07 intégrée | ORION, Calendar + Month ; période et événements synthétiques vérifiés |
| Contrats | Lire période, quotité et état sur la fiche personne | `user-guide/people/work-and-contracts.md` | P1 | Validé | P1-01 intégrée | Contrat doctoral lié à ORION vérifié ; actions selon droits |
| Absences | Consulter les absences d’une personne | `user-guide/people/leave.md` | P1 | Validé | P1-03 intégrée | Deux absences de démonstration vérifiées en vue Table ; mode Calendar décrit |
| Absences | Créer ou corriger une absence | À définir | P1 | À analyser | À définir | React confirmé mais actions selon droits ; hors de cette passe |
| Financement | Trouver un fonds, lire période, consommation et disponible | `user-guide/finance/view-a-fund.md` | P1 | Validé | P1-08/10 intégrées ; P1-14/15 conditionnelles | Projet → Funds ; sélection du fonds ; ORION et DM-ORION-BRIDGE contrôlés sur P1-08/10 |
| Budgets | Lire affectation, consommé et disponible | `user-guide/finance/budgets-and-expenses.md` | P1 | Validé | P1-11 intégrée | Section Budgets du projet ; aucune formule interne affirmée |
| Contributions | Lire période et affectation RH | `user-guide/finance/budgets-and-expenses.md` | P1 | Validé | Texte vérifié ; aucune capture dédiée nécessaire | Section distincte de Budgets ; détails accessibles selon visibilité |
| Dépenses | Filtrer et lire une dépense | `user-guide/finance/budgets-and-expenses.md` | P1 | Validé | P1-12 intégrée | Dépenses du fonds/budget ; saisie hors périmètre, actions selon capacités |
| Explorateur de fonds | Filtrer et comparer les lignes financières visibles | `user-guide/finance/fund-explorer.md` | P1 | Validé | P1-13 intégrée | Lignes de fonds, pas fiches de fonds ; visibilité projets + fonds |
| Évolution financière | Repérer le widget mensuel des dépenses visibles | `user-guide/dashboards/use-your-dashboard.md` | P1 | Rédigé ; capture différée | P1-16 non nécessaire | Widget du modèle Project, absent des trois modèles personnels préconfigurés ; aucune courbe de fonds autonome |
| Dashboard | Choisir et lire son tableau personnel | `user-guide/dashboards/use-your-dashboard.md` | P1 | Rédigé ; captures bloquées | P1-17 prête ; P1-18/19 bloquées | Trois modèles personnels précréés ; `leader` et `labmanager` manquent dans Capture |
| Dashboard | Choisir un modèle à la première utilisation | `user-guide/dashboards/use-your-dashboard.md` | P1 | Rédigé ; capture non nécessaire | Aucune dédiée | Vue React confirmée quand aucun tableau personnel n’existe ; non visible sur les comptes démo préconfigurés |
| Dashboard | Ajouter et organiser des widgets | `user-guide/dashboards/customize-your-dashboard.md` | P1 | Rédigé ; capture non nécessaire | Aucune dédiée | Customize, catalogue, ajout/retrait, déplacement/redimensionnement desktop et sauvegarde confirmés dans React ; pas de remise à zéro |
| Dashboard Project | Repérer Expense evolution | `user-guide/dashboards/use-your-dashboard.md` | P1 | Rédigé ; capture différée | Aucune pour les trois modèles personnels | Widget préconfiguré dans le template Project ; aucune courbe de fonds autonome |
| Exports | Exporter une liste ou une fiche | Exporter et imprimer | P1 | À analyser | Menu export | Formats et rapports à vérifier |
| Impression | Imprimer Gantt ou calendrier | Exporter et imprimer | P1 | À faire | Aperçu impression | Données de démonstration |
| Recherche avancée | Composer une requête et utiliser suggestions | Recherche avancée | P2 | À analyser | Recherche | Autocomplétion attend validation navigateur |
| Gantt et dépendances | Lire la chronologie et les liens | Lire Gantt et dépendances | P2 | À faire | Gantt | Dépendances déclaratives, sans replanification automatique |
| Dashboard | Approfondir configuration, présentation et widgets optionnels | À définir | P2 | À analyser | Éditeur Dashboard | La personnalisation de base est décrite en P1 ; variantes et plugins restent à vérifier |
| Contrats transversaux | Explorer tous les contrats visibles | Contrats et finances | P2 | À analyser | Outil Contrats | Validation navigateur attendue |
| Finances transversales | Approfondir Budget explorer et l’outil Expenses | À définir | P2 | À analyser | Outils financiers | Fund explorer est déjà rédigé en P1 Finance ; lecture seule globale |
| Imports | Préparer, contrôler puis valider un import | Importer | P2 | À analyser | Aperçu d'import | Profils disponibles à vérifier |
| Équipes | Consulter membres, projets, absences et budget | Calendriers, organismes et équipes | P3 | À analyser | Fiche Team | Validation navigateur attendue |
| Institutions/financeurs | Retrouver contacts, projets et contrats liés | Calendriers, organismes et équipes | P3 | À analyser | Fiche Organisation | Contacts selon données disponibles |
| Calendrier global | Filtrer période, ressource et événements | Calendriers, organismes et équipes | P3 | À analyser | Vue Ressources | Plugins peuvent ajouter des événements |
| GenericInfo / notes | Ajouter une information ou note si autorisé | Glossaire et variantes | P3 | À analyser | Fiche Employee | Champs configurables ; droits contextuels |
| Organigramme | Explorer hiérarchie et imprimer | Calendriers, organismes et équipes | P3 | À analyser | Organigramme | Vérifier l'écran cible |
| Favoris/abonnements | Suivre un objet et régler notifications | Favoris, notifications, réglages | P3 | À analyser | Réglages | Visibilité et réglages personnels |
| Rapports | Choisir et produire un rapport historique | Rapports et formats | P3 | À analyser | À déterminer | Parcours legacy à confirmer |
| Plugins | Comprendre une fonction optionnelle visible | Glossaire et variantes | P3 | À analyser | Selon plugin | Ne pas promettre présence universelle |
