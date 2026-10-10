# Audit initial et proposition — 6 octobre 2026

## Périmètre et niveau de preuve

**Vérifié dans le dépôt documentaire :** fichiers MkDocs, navigation, pages et assets. **Confirmé par mémoire de migration :** état fonctionnel et routes consignés dans `docs/react-migration/MATRIX.md` et passages ciblés de `STATUS.md` du dépôt applicatif. **Propositions :** priorités, regroupements et pages cibles ; à valider avec le responsable. Aucune validation systématique sur navigateur ni audit exhaustif du code n'a été mené.

## État publié

MkDocs + thème Material 9.5.4, hébergé par ReadTheDocs (`.readthedocs.yaml` v2, Python 3.10). Source `docs/`, entrée `index.md`, navigation explicite dans `mkdocs.yml` : LabsManager, Employee, Project, Plugins, Other. Il n'y a pas de `toctree` Sphinx actif. Extensions Markdown : attr_list, md_in_html, admonition, détails, superfences, emoji Material, highlight, inlinehilite, snippets. Dépendances dans `docs/requirements.txt` ; CSS `docs/css/base.css`, logo/favicon et quatre captures dans `docs/assets/`. `docs/.overrides/.icons/fontawesome/` contient un volumineux lot d'icônes ; aucun mécanisme de génération documentaire identifié. `docs/Makefile` et `make.bat` sont des restes Sphinx ; `README.rst` décrit encore un tutoriel Sphinx. Le `pyproject.toml` paraît un résidu de template, pas une source de navigation MkDocs.

| Page/section actuelle | Traitement proposé | Motif |
|---|---|---|
| `index.md` | Remplacer, garder l'intention introductive et l'identité | Présentation vague, capture d'un ancien hub, peu de chemins d'action |
| `general/concept.md` | Réorganiser et réécrire ; réutiliser les relations Employee/Project/Fund | Liste de modèles et termes internes ; liens à vérifier |
| `general/shared_process.md` | Partiellement réutiliser pour filtres, exports, favoris ; remplacer les modes d'emploi | Capture et actions décrivent l'ancienne interface ; calendrier ancien |
| `general/employee.md` | Remplacer ; extraire quelques concepts RH | Panneaux et menus legacy, édition Employee annoncée alors qu'elle est différée en React |
| `general/project.md` | Remplacer | Fichier vide |
| `general/employee_export.md`, `general/project_export.md` | Scinder : parcours export utilisateur à vérifier ; syntaxe de modèles vers référence avancée | Référence de variables très technique et possiblement ancienne |
| `general/installation.md` | Réserver au futur volet administrateur ; vérifier avant réemploi | Long exemple de déploiement, sans utilité directe au nouvel utilisateur |
| `general/rights_mngt.md` | Revoir plus tard pour administration ; réutiliser seulement l'idée de visibilité variable | Profils et permissions décrits globalement, sans nuance objet/capability |
| `plugins/plugins.md`, `calendarmixin.md`, `mailsubscriptionmixin.md`, `schedulemixin.md` | Réserver aux développeurs ; vérifier les contrats actuels | APIs mixin historiques, trop techniques pour la documentation utilisateur |
| `other/libraries.md` | Actualiser ou retirer de la navigation utilisateur | Inventaire de dépendances ancien |
| `other/credits.md` | Conserver après vérification des crédits | Contenu éditorial distinct des parcours |

Les quatre captures `hub.png`, `list_tools.png`, `panel_tool.png`, `action.png` semblent liées à l'ancienne interface ; vérifier avant toute réutilisation. `icon.png` et `favicon.png` peuvent rester comme identité graphique. La documentation est surtout en anglais, avec des libellés parfois incohérents, tandis que l'interface React possède des libellés français/anglais.

## Écarts principaux

Les parcours React absents couvrent accueil/récents, recherche globale, dashboard, équipes, organismes et contacts, planning/Gantt, calendriers, contrats transversaux, financements et dépenses, notes, imports, outils, préférences. La fiche Employee publiée décrit des panneaux et actions legacy ; la fiche Project ne décrit rien. Les permissions sont présentées comme rôles globaux alors que les capacités sont contextuelles. Les captures ne peuvent pas guider dans React. Certains parcours React sont encore en attente de validation navigateur dans la mémoire applicative ; vérifier la version déployée avant rédaction impérative.

## Cartographie des besoins utilisateur

| Domaine | Actions/questions à couvrir |
|---|---|
| Prise en main, accueil, navigation | Se connecter, comprendre l'accueil, rejoindre une rubrique, revenir à un élément récent, savoir pourquoi une action manque |
| Recherche et listes | Rechercher partout, choisir un résultat, filtrer/trier une liste, partager ou retrouver une sélection |
| Employés, équipes | Trouver une personne/équipe, lire identité/statut/hiérarchie, participations, charge et notes |
| Contrats et absences | Consulter périodes/quotités, repérer échéance, saisir ou corriger une absence selon droits, lire le calendrier |
| Projets et participants | Trouver/créer un projet si autorisé, consulter paramètres, participants, contrats et notes |
| Tâches et jalons | Voir le planning, filtrer, suivre avancement/échéance, éditer selon capacité, lire dépendances et Gantt |
| Financements, budgets, contributions, dépenses | Suivre un Fund, comprendre les montants et périodes, voir Budget/Contribution, rechercher et justifier une Expense |
| Institutions, financeurs, contacts | Retrouver une organisation, consulter projets/contrats/contacts liés |
| Calendriers | Choisir période et portée Employee/Project/Team/global, filtrer événements et ressources, imprimer |
| Dashboard, favoris, abonnements | Choisir/personnaliser un tableau, interpréter les widgets, retrouver favoris, régler notifications |
| Informations complémentaires et notes | Lire/ajouter un champ configuré ou une note si autorisé ; comprendre leur portée |
| Explorateurs, outils, imports, exports, impressions | Explorer contrats/finances, importer avec aperçu, exporter liste/fiche, imprimer Gantt/calendrier |

## Parcours et priorités proposés

**Essentiels :** prendre en main ; retrouver une information ; consulter un employé ; consulter un projet ; comprendre les droits visibles. **Fréquents :** suivre participants, tâches et jalons ; consulter contrats et absences ; lire calendrier ; suivre financement/budget/dépense ; utiliser son dashboard ; filtrer et exporter. **Avancés :** personnaliser dashboard, requêtes de recherche avancées, Gantt/dépendances, outils financiers et imports. **Occasionnels :** organiser favoris/notifications, gérer informations complémentaires et notes, consulter organismes/contacts, imprimer, rapports historiques.

Concepts à expliquer : visibilité et droit d'agir (définition courte + exemple) ; Employee/Project/Participant/Contract et quotité (exemple + schéma léger) ; tâche versus jalon et dépendance (exemple + capture Gantt) ; Fund → Budget → Expense, Contribution et montants signés (page dédiée + schéma + exemple) ; calendrier et vues par ressource (capture) ; champs GenericInfo, notes et plugins (définition courte + exemple) ; dashboard personnel versus projet (capture + exemple). Les intitulés finaux sont à confirmer avec les utilisateurs métier.

## Architecture utilisateur cible proposée

Le tableau associe chaque page à son objectif, son public et ses tâches. Les titres sont des propositions, pas encore des pages publiées. P0–P3 forment le MVP progressif.

| Groupe / page proposée | Objectif et tâches | Public | Priorité |
|---|---|---|---|
| Commencer / Premiers pas | Accéder, lire l'accueil, ouvrir une fiche, reconnaître les actions disponibles | Tous | P0 |
| Commencer / Se repérer | Navigation, sous-routes, retour, listes, droits visibles | Tous | P0 |
| Trouver / Rechercher et filtrer | Recherche globale, résultats, filtres simples | Tous | P0 |
| Personnes / Consulter un employé | Trouver, lire identité, statuts, projets, contrats, absences, financement | Tous | P0 |
| Projets / Consulter un projet | Ouvrir fiche, repérer participants, planning, financement | Tous | P0 |
| Projets / Suivre les participants | Lire participation et charge ; modifier si autorisé | Responsables, gestionnaires | P1 |
| Projets / Suivre tâches et jalons | Tableau, échéances, statuts, édition selon droits | Responsables, collaborateurs | P1 |
| Projets / Consulter le calendrier | Période, filtres, événements du projet | Tous | P1 |
| Financement / Suivre un financement | Fund, sources, montants, dépenses | Responsables, gestionnaires | P1 |
| Financement / Lire budgets et contributions | Affectations, disponible, consommation et quotités | Responsables, gestionnaires | P1 |
| Personnes / Consulter contrats et absences | Périodes, quotités, calendrier, mutation selon droits | Collaborateurs, gestionnaires | P1 |
| Espace personnel / Utiliser ses tableaux de bord | Choisir, lire widgets, retrouver tableaux | Tous | P1 |
| Partager / Exporter et imprimer | Exports de listes/fiches, impression de vues | Tous selon droits | P1 |
| Trouver / Recherche avancée | Syntaxe, suggestions et cas d'usage | Utilisateurs réguliers | P2 |
| Projets / Lire Gantt et dépendances | Charge, échéances, liens déclaratifs | Responsables | P2 |
| Espace personnel / Personnaliser un tableau | Modèles, widgets, grille et présentation | Tous | P2 |
| Explorer / Contrats et finances | Outils transversaux, filtres et détail | Gestionnaires | P2 |
| Données / Importer | Modèle, aperçu, erreurs, validation | Gestionnaires autorisés | P2 |
| Référence / Glossaire et variantes | Termes, fonctions optionnelles, paramètres locaux | Tous | P3 |
| Référence / Calendriers, organismes et équipes | Cas transversaux et relations | Utilisateurs concernés | P3 |
| Référence / Favoris, notifications, réglages | Préférences et abonnements | Tous | P3 |
| Référence / Rapports et formats | Rapports legacy et formats détaillés, après vérification | Utilisateurs concernés | P3 |

## Captures et maintenance

Le registre `SCREENSHOTS.md` précise écran, contenu, but et annotation. Un schéma est préférable pour les relations financières ; aucune campagne de captures lancée. Automatiser ou vérifier : liens et navigation MkDocs, pages orphelines, build strict, existence des routes, noms d'écrans, état des exports, inventaire des plugins et capacités, dates/captures de version. Les listes de champs configurables, permissions, navigation, widgets et partage React/legacy changent vite : les vérifier sur une version cible et éviter de recopier des catalogues exhaustifs dans la prose. Les parcours, exemples métier, choix de vocabulaire et explications restent éditoriaux.

Plus tard, le volet **administration** devra couvrir installation/mise à jour, utilisateurs/groupes/permissions, paramètres, listes configurables, plugins, notifications, sauvegarde et exploitation. Le volet **développement** devra couvrir architecture React/Django/API, contrats de capacités, tests, contributions, plugins et génération de rapports. Aucun de ces volets n'est détaillé ici.

## Arbitrages avant rédaction

Choisir langue principale et politique bilingue ; identifier les profils métier représentatifs et un jeu de démonstration ; valider les intitulés et P0 avec utilisateurs ; fixer la version/déploiement de référence et le traitement des fonctions React non encore validées ; décider de la redirection ou conservation des URL publiées ; confirmer quels rapports legacy et plugins sont réellement destinés aux utilisateurs.
