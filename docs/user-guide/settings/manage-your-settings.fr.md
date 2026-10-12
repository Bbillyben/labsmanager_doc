# Gérer vos paramètres

Ouvrez le menu de votre compte en haut à droite et choisissez **User settings**. Vous pouvez aussi accéder directement à `/app/settings/user`. L’espace des paramètres personnels comporte cinq sections : **User settings**, **Interface**, **Notifications**, **Favorites and subscriptions** et **Stale alerts**. Sélectionnez une section dans sa navigation. Toutes les sections sont accessibles aux utilisateurs connectés ; les valeurs et les modifications enregistrées appartiennent à votre compte.

Vous pouvez également voir **Lists** ou **Administration** dans cette navigation. Ces espaces gèrent les données de référence partagées ou les paramètres de toute l’installation et ne font pas partie des préférences personnelles. Administration n’apparaît que pour les comptes du personnel autorisé.

## Compte et adresses e-mail

La section **User settings** affiche votre nom d’utilisateur, votre nom, votre dernière connexion et la fiche Employee liée, si elle existe. Ces informations sont présentées à titre indicatif ; cette page ne permet pas de les modifier.

![Paramètres utilisateur avec le résumé du compte et les adresses e-mail](../../assets/screenshots/settings/user.png)

Choisissez **Change password** (ou **Set password** si vous n’en avez pas) pour ouvrir un formulaire. Saisissez votre mot de passe actuel si demandé, puis deux fois le nouveau et choisissez **Save**. Les erreurs de validation s’affichent dans le formulaire. Selon les règles de connexion de votre compte, vous pouvez être déconnecté après la modification et devoir vous reconnecter.

La liste **Email addresses** marque chaque adresse comme principale ou secondaire, vérifiée ou non vérifiée. Si **Add email** est disponible, saisissez une adresse et envoyez le formulaire. Le menu d’actions d’une adresse peut permettre de définir comme principale une adresse secondaire vérifiée, de renvoyer la vérification ou de supprimer une adresse secondaire. Les actions disponibles dépendent de l’état de l’adresse et des règles du compte. La suppression d’une adresse demande confirmation ; l’adresse principale ne peut pas être supprimée ici.

## Interface

Ouvrez **Interface** pour choisir la page d’arrivée après connexion, l’affichage des anciennes affiliations à des organisations, le fournisseur de carte pour les liens de localisation et le thème de l’application. La page d’arrivée, le fournisseur de carte et le thème utilisent des listes de sélection ; l’option d’organisation est un interrupteur. Les thèmes proposés sont **Light** et **Dark**. Cette section ne modifie pas le mode d’affichage du calendrier global.

![Préférences Interface avec page d’arrivée, interrupteur d’organisation, fournisseur de carte et thème](../../assets/screenshots/settings/interface.png)

Les interrupteurs et les sélections sont enregistrés dès leur modification. Le thème s’applique à l’interface lorsque son enregistrement réussit. La page affiche brièvement un état d’enregistrement en cours ou terminé. Si une valeur est refusée, elle affiche une erreur et conserve la dernière valeur enregistrée.

## Notifications

Ouvrez **Notifications** pour gérer les notifications automatiques par e-mail. La section regroupe ces commandes personnelles :

| Domaine | Commandes |
| --- | --- |
| Envoi | Interrupteur des notifications par e-mail ; sélections de fréquence et de langue des rapports. |
| Jalons | Interrupteurs des événements et des jalons suivis ; champs numériques pour le seuil d’ancienneté, l’intervalle de répétition, la répétition du rapport et l’horizon des échéances proches. |
| Personnes et projets | Interrupteurs de participation aux projets, d’événements concernant les collaborateurs et des nouveaux collaborateurs. |
| Congés | Interrupteur d’inclusion des congés ; choix de présentation Calendar/List et de période ; interrupteur pour inclure les collaborateurs sans congé dans la présentation calendrier. |

Une description figure à côté de chaque commande. Certains paramètres déterminent les informations incluses dans les e-mails de notification ; l’interrupteur principal contrôle l’envoi automatique des notifications.

![Préférences Notifications avec commandes d’e-mail, de langue, de jalons et de fréquence](../../assets/screenshots/settings/notifications.png)

Le choix de présentation des congés sélectionne **Calendar** ou **List** dans l’e-mail de notification. Il ne fait pas passer le [calendrier global](../calendar/use-the-calendar.md) de la vue Calendar à la vue Resources. Choisissez **Send test notification** pour demander un e-mail, ou **Preview notification** pour ouvrir le message mis en forme dans un nouvel onglet. Autorisez les fenêtres surgissantes si l’aperçu est bloqué. Ces actions de test sont distinctes de l’enregistrement d’une préférence.

Les interrupteurs et les listes sont enregistrés immédiatement. Pour un champ numérique ou textuel, quittez le champ ou appuyez sur Entrée pour enregistrer. La page indique l’enregistrement en cours, terminé ou en erreur. Votre installation doit pouvoir envoyer des e-mails pour que la notification de test arrive.

## Favoris et abonnements

La section **Favorites and subscriptions** répertorie les fiches que vous avez marquées comme favorites ou auxquelles vous êtes abonné. Suivez un lien pour ouvrir la fiche, ou choisissez **Remove** à côté d’une entrée pour supprimer immédiatement ce favori ou cet abonnement. Une liste vide affiche un état vide. Sur les fiches qui le permettent, les commandes en forme d’étoile et de cloche ajoutent ou retirent les mêmes préférences. Les fiches que vous pouvez suivre dépendent de celles qui vous sont accessibles.

## Alertes d’ancienneté et tableaux de bord

La section **Stale alerts** comporte quatre champs de mois non négatifs pour les contrats, projets, jalons et financements. Ils définissent les horizons de recherche utilisés par les [résumés des tableaux de bord](../dashboards/use-your-dashboard.md) de votre compte. Saisissez un nombre entier, puis quittez le champ ou appuyez sur Entrée pour enregistrer. Une valeur invalide est refusée et une erreur s’affiche. Il s’agit de préférences personnelles concernant les données du tableau de bord ; le choix et la disposition des widgets se gèrent [sur le tableau de bord](../dashboards/customize-your-dashboard.md).

Ces cinq sections ne comprennent pas de préférence distincte pour la vue du calendrier. Choisissez le mode Calendar ou Resources sur la [page Calendars](../calendar/use-the-calendar.md) lorsque vous l’utilisez. Le choix Calendar/List de l’e-mail de notification ne change que la présentation des congés dans cet e-mail.
