# Conventions éditoriales initiales

- Commencer par le but et les prérequis de la tâche, puis guider l'action et expliquer le résultat attendu.
- Employer les mots de l'utilisateur ; éviter les noms de modèles, d'API et le jargon technique sans utilité pour la tâche.
- Expliquer les concepts métier avant les détails d'interface ; relier les termes Fund, Budget, Contribution et Expense à un exemple concret avant leur emploi procédural.
- Distinguer les fonctions standard, celles qui exigent des droits et celles qui dépendent d'un plugin ou de la configuration.
- Ne documenter comme disponibles que les comportements vérifiés sur la version cible. Préférer « si l'action est disponible » quand les capacités varient.
- Utiliser seulement des données de démonstration ou non sensibles dans exemples et captures.

L’anglais est la langue source ; les traductions françaises utilisent le même chemin avec le suffixe `.fr.md`. Une page pilote commence par le besoin utilisateur, emploie des verbes d’action, puis propose une courte suite de parcours. Les captures utilisent le fichier PNG natif et une largeur responsive (100 % du contenu disponible), sans agrandissement au-delà de sa résolution native. Une bordure discrète sépare l’interface du fond ; une légende courte est ajoutée seulement si elle apporte un contexte. Capturer la vue entière pour situer la navigation, puis une région ciblée pour expliquer une action. Éviter le recadrage manuel après capture.

## Parité des traductions du guide utilisateur

L’anglais reste la source des pages utilisateur publiées. Lors de chaque création ou modification d’une page `docs/user-guide/*.md` (ou de la page d’accueil utilisateur `docs/index.md`), créer ou mettre à jour dans le même changement sa version `.fr.md` au même emplacement. Conserver le sens, les niveaux de titres, les liens, les références d’images, les exemples et les limites liées aux droits ou plugins. Traduire les explications et les textes alternatifs ; garder les libellés de l’interface en anglais tant que l’interface les affiche ainsi. Vérifier la parité des pages et les builds EN/FR avant de clore le lot. Les pages Admin, Developer et legacy ne font pas partie de cette règle du guide utilisateur.
