# Gestion de la posture de sécurité

L’équipe de sécurité de Contoso souhaite améliorer l’état de sa sécurité à l’aide du Niveau de sécurité Microsoft, un outil qui fournit des recommandations et des conseils sur la façon de réduire la surface d’attaque et de se protéger contre les menaces.

L’équipe de sécurité examine et délègue les actions recommandées par le Niveau de sécurité à ses membres étendus de l’équipe (ambassadeurs de sécurité) qui gèrent le statut et le plan d’action associés aux actions d’amélioration. L’équipe de sécurité souhaite également contrôler l’accès aux informations sur l’état de la sécurité et aux sources de données qui les alimentent. Joni Shermann est l’un des ambassadeurs de sécurité et a besoin d’un accès à Gestion de l’exposition.

Récemment, il a été signalé que des collaborateurs non invités étaient automatiquement admis dans des appels Teams auxquels ils n’avaient pas été directement invités.  En raison de la nature sensible et confidentielle des appels, l’équipe de sécurité souhaite contrôler cet aspect.

## Partie 1 : concevoir une solution (obligatoire)

### Approche de conception

L’onglet Actions recommandées du Niveau de sécurité Microsoft liste les recommandations de sécurité associées aux surfaces d’attaque potentielles. Ces actions peuvent être partagées/déléguées.

Les équipes de sécurité doivent contrôler l’accès aux informations sur l’état de la sécurité de l’organisation et aux sources de données spécifiques qui les alimentent. Le modèle de contrôle d’accès en fonction du rôle unifié (RBAC) Microsoft Defender XDR offre une expérience de gestion des autorisations unique et fournit un espace centralisé aux équipes d’administration pour contrôler les autorisations utilisateur des différentes solutions de sécurité.

Pour vous assurer que les ambassadeurs de sécurité disposent des autorisations de rôle nécessaires, vous devez créer un rôle personnalisé. Pour que le portail de sécurité Microsoft Defender XDR commence à appliquer les autorisations et les affectations configurées dans vos nouveaux rôles personnalisés ou importés, vous devez activer le modèle de RBAC unifié Microsoft Defender XDR pour certaines ou toutes vos charges de travail.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Joni Shermann gérera les actions et le statut associés aux recommandations du Niveau de sécurité. |Gestion de l’exposition - Niveau de sécurité et RBAC unifié Defender XDR | Créez un rôle pour gérer l’état de la sécurité et accorder l’accès à Joni Shermann. |
|Contrôlez l’accès aux informations sur l’état de la sécurité et aux sources de données qui les alimentent. | RBAC unifié Microsoft Defender XDR | Activez le RBAC unifié Microsoft Defender XDR pour un rôle personnalisé. |
|Partager une action recommandée par le Niveau de sécurité |Degré de sécurisation | Partagez des actions recommandées. |

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : créer un rôle personnalisé pour gérer l’état de la sécurité pour Gestion de l’exposition

Dans cette tâche, vous allez configurer un rôle personnalisé axé sur l’état de la sécurité et, plus précisément, sur Gestion de l’exposition. Dans le cadre du rôle personnalisé, vous accorderez à Joni Shermann l’accès à la source de données pour Gestion de l’exposition.

1. Connectez-vous à la machine virtuelle cliente Windows **LON-SC1** avec le compte **Administrateur** local. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresses, accédez à **`https://security.microsoft.com`** et connectez-vous à **Microsoft Defender** tant qu’administrateur MOD **admin@WWLxZZZZZZ.onmicrosoft.com** (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.
1. Dans la boîte de dialogue **Rester connecté ?**, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
1. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant **Jamais**, pour ne pas enregistrer les informations d’identification d’administration générale par défaut dans votre navigateur.
1. Si vous voyez une zone d’informations en haut à droite de l’écran qui indique **Gérer l’authentification multifacteur**, fermez-la en cliquant sur le **X**.
1. Dans le volet de navigation de gauche, développez **Système**, puis sélectionnez **Autorisations**.
1. Si c’est la première fois que vous accédez aux paramètres de Microsoft Defender, vous devrez patienter quelques minutes pendant que Defender prépare de nouveaux espaces pour vos données et les connecte.  Une fois cette opération terminée, actualisez la page des autorisations jusqu’à ce que vous voyiez une liste incluant Microsoft Defender XDR, Microsoft Entra ID, Rôles et groupes de points de terminaison, Rôles e-mail et collaboration, et Cloud Apps. L’affichage de tous les éléments peut prendre un certain temps.
1. Sous **Microsoft Defender XDR(1)**, sélectionnez **Rôles**.
1. Sélectionnez **Créer un rôle personnalisé**.
1. Dans le champ Nom de rôle, entrez **`SecureScore Manager`** et sélectionnez **Suivant**.
1. Sélectionnez **Posture de sécurité**.
1. Dans la fenêtre État de la sécurité :
    - Sélectionnez **Sélectionner des autorisations personnalisées**.
    - Sous Gestion de l’état, sélectionnez **Sélectionner des autorisations personnalisées**.
    - Sélectionnez **Gestion de l’exposition (gérer)**.
    - Sélectionnez **Appliquer**.
    - Cliquez sur **Suivant**.
1. Sur la page **Attribuer des utilisateurs et des sources de données**, sélectionnez **Ajouter une attribution**, puis renseignez les champs comme suit :
    - Nom de l’attribution : **`ExposureManagement`**
    - Attribuer des utilisateurs et un groupe : entrez et sélectionnez **`Joni Sherman`**.
    - Sous **Sources de données**, sélectionnez le menu déroulant pour afficher la liste des sources de données disponibles. Sélectionnez uniquement **Sécurité Microsoft - Gestion de l’exposition**.  Si d’autres sources de données apparaissent, désélectionnez-les.
    - Sélectionnez **Ajouter**.
    - Sélectionnez **Suivant**.
1. Sur la page Vérifier et terminer, vérifiez les paramètres, sélectionnez **Soumettre**, puis **Terminé**.
1. Vous devriez vous trouver sur la page **Autorisations et rôles** et voir le rôle personnalisé que vous venez de créer. Gardez cet onglet ouvert, car vous l’utilisez dans la prochaine tâche.

Vous avez correctement configuré un rôle personnalisé pour l’état de la sécurité qui accorde à Joni Shermann l’accès à la source de données de Gestion de l’exposition.

### Tâche 2 : activer le RBAC unifié Defender XDR pour des charges de travail spécifiques

Pour que le portail de sécurité Microsoft Defender XDR commence à appliquer les autorisations et les affectations configurées dans vos nouveaux rôles personnalisés, vous devez activer le modèle de RBAC unifié Microsoft Defender XDR pour vos charges de travail.

Lorsque vous activez certaines ou toutes vos charges de travail pour utiliser le nouveau modèle d’autorisation, les rôles et autorisations de ces charges de travail sont entièrement contrôlés par le modèle de RBAC unifié Microsoft Defender XDR dans le portail Microsoft Defender.

Dans cette tâche, vous allez explorer la page sur laquelle les charges de travail sont activées.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender sur la page **Autorisations et rôles**. Le rôle personnalisé que vous venez de créer devrait s’afficher.
1. Lisez les informations dans la bannière grise. Certains rôles ne s’appliquent pas encore, car vous n’avez pas activé toutes les charges de travail. Sélectionnez **Activer les charges de travail**.
1. Lisez la description sous **Activer le contrôle d’accès en fonction du rôle unifié**.  Lorsque vous activez certaines ou toutes vos charges de travail pour utiliser le nouveau modèle d’autorisation, les rôles et autorisations de ces charges de travail sont entièrement contrôlés par le modèle de RBAC unifié Microsoft Defender XDR dans le portail Microsoft Defender.
1. Pour cet exercice, la source de données de Gestion de l’exposition est activée par défaut, c’est pourquoi il n’existe aucun paramètre pour activer cette charge de travail. Si vous aviez créé un rôle personnalisé incluant des autorisations pour d’autres charges de travail, telles qu’Office 365 ou la gestion des appareils et des vulnérabilités, par exemple, vous devriez activer ces charges de travail spécifiques pour activer le rôle personnalisé, dans le cadre du RBAC unifié.

Vous avez appris à activer le modèle de RBAC unifié Microsoft Defender XDR pour certaines ou toutes vos charges de travail.

### Tâche 3 : partager une action recommandée

Partagez une action recommandée par le Niveau de sécurité Microsoft. Dans cette tâche, vous allez publier l’action sur un canal Teams. En le publiant sur Teams, les utilisateurs du canal verront une notification, mais n’auront pas accès à la source de données pour modifier le statut ou gérer l’action. Seul Joni Shermann, qui est membre du canal Teams et qui dispose d’autorisations de rôle, peut accéder à l’action recommandée.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender XDR.
1. Dans le volet de navigation de gauche, développez **Gestion de l’exposition**, puis sélectionnez **Niveau de sécurité**.
1. Sélectionnez l’onglet **Actions recommandées**.
1. Recherchez et sélectionnez **`Only invited users should be automatically admitted to Teams meetings`**.
1. Sélectionnez **Partager**, puis, dans le menu déroulant, sélectionnez **Microsoft Teams**.
1. Dans l e champ**Équipe**, sélectionnez **Équipe de projet Mark 8** et, dans le champ **Canal**, sélectionnez **Canal Recherche et développement**.
1. Sélectionnez **Publier un message dans Teams**.

Joni Sherman et son équipe de projet Mark 8 seront informés de l’action recommandée dans le canal Teams.

### Tâche 4 : gérer les recommandations

Comme Joni Sherman, vous avez reçu la notification Teams qu’une action spécifique pour améliorer l’état de la sécurité de l’organisation a été recommandée.  En tant que membre étendu de l’équipe de sécurité, vous disposez des autorisations de rôle pour gérer l’action recommandée et documenter la solution.

Dans cette tâche, vous allez gérer les actions recommandées et documenter vos solutions.

1. Ouvrez une fenêtre Microsoft Edge InPrivate, accédez à **`https://office.com`** et connectez-vous en tant que **JoniS@WWLxZZZZZZ.onmicrosoft.com**.
1. Si la page de destination apparaît floue, actualisez la page.
1. Sélectionnez l’icône du lanceur d’applications, située à gauche de la bannière supérieure qui indique Contoso Electronics, puis sélectionnez **Teams**.
1. Dans la fenêtre Bienvenue dans Teams, sélectionnez **Démarrer**. La configuration de Teams peut prendre une minute ou deux. Si un écran de code QR Teams pour mobile s’affiche, fermez-le.
1. Ouvrez Teams. Pour **Équipe de projet Mark 8**, sélectionnez **Afficher tous les canaux**, puis **Recherche et développement**.
1. Examinez le message publié de la tâche précédente.
1. Dans le message publié, sélectionnez le lien **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.  Étant donné que vous, Joni Shermann, avez reçu l’autorisation par le biais du rôle personnalisé, vous pouvez accéder au Niveau de sécurité.  D’autres membres de l’équipe de projet Mark 8 peuvent voir la publication, mais n’ont pas accès au Niveau de sécurité.
1. Sélectionnez **Modifier l’état et le plan d’action**.
1. Cochez **Résolu par le biais d’un tiers**.
1. Ajoutez une note **Actuellement sécurisé** dans le champ **Plan d’action**.
1. Sélectionnez **Enregistrer et fermer**.
1. Fermez les onglets du navigateur inPrivate.

En tant que Joni Shermann, vous avez correctement modifié le statut de l’action recommandée.

### Tâche 5 (facultative) : Adele Vance accède à la publication Teams

Dans cette tâche, Adele Vance accède au canal de l’équipe de projet Mark 8 et sélectionne le lien dans le message publié.

1. Ouvrez une fenêtre Microsoft Edge InPrivate, accédez à **`https://office.com`** et connectez-vous en tant que Adele Vance, **AdeleV@WWLxZZZZZZ.onmicrosoft.com**.
1. Si la page de destination apparaît floue, actualisez la page.
1. Sélectionnez l’icône du lanceur d’applications, située à gauche de la bannière supérieure qui indique Contoso Electronics, puis sélectionnez **Teams**.
1. Dans la fenêtre Bienvenue dans Teams, sélectionnez **Démarrer**.
1. Ouvrez Teams. Pour **Équipe de projet Mark 8**, sélectionnez **Afficher tous les canaux**, puis **Recherche et développement**.
1. Examinez le message publié de la tâche précédente.
1. Sélectionnez le lien dans le message publié **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.
1. Vous accédez directement au Niveau de sécurité Microsoft, mais vous n’avez pas l’autorisation d’accéder à ces données, car Adele Vance n’a pas été ajoutée en tant que membre au rôle personnalisé que vous avez créé.
1. Fermez les onglets du navigateur InPrivate.

Dans cette tâche, vous avez confirmé que les membres du projet Mark 8 peuvent voir le message publié pour l’action recommandée afin d’améliorer l’état de la sécurité de l’organisation, mais seuls les associés qui ont été ajoutés au rôle personnalisé peuvent accéder aux informations du Niveau de sécurité.
