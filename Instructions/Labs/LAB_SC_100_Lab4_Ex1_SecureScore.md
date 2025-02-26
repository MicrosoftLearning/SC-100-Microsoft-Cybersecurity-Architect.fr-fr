# Labo 4 - Exercice 1 - Gestion de l’état de la sécurité

Contoso souhaite améliorer l’état de sa sécurité à l’aide du Niveau de sécurité Microsoft, un outil qui fournit des recommandations et des conseils sur la façon de réduire la surface d’attaque et de se protéger contre les menaces. Contoso dispose d’une équipe de sécurité dédiée qui gère le tableau de bord Niveau de sécurité et affecte des actions à différentes équipes de produits en fonction de leurs rôles et responsabilités. L’une des équipes de produits, l’équipe de projet Mark 8, est responsable de la gestion des périphériques mobiles et doit s’assurer que les appareils se verrouillent après une période d’inactivité afin d’empêcher les accès non autorisés.

## Partie 1 : concevoir une solution (obligatoire)

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Obtenir plus de recommandations pour augmenter l’état de la sécurité
- Accorder un accès limité aux recommandations 
- Informer l’équipe responsable

Le Niveau de sécurité Microsoft évalue l’état de la sécurité d’une organisation sur toutes les charges de travail Microsoft 365. Il fournit une visibilité centralisée, des informations hiérarchisés par menace et des contrôles complets pour améliorer la protection contre les cyberattaques et optimiser la cybersécurité.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Ajouter d’autres recommandations pour augmenter l’état de la sécurité | Sources de données supplémentaires | Activer des sources « hors charge de travail » supplémentaires |
|Accorder un accès limité aux recommandations |Autorisation et rôles Defender XDR |Accorder un accès spécifique à Joni Shermann |
|Informer l’équipe responsable |Degré de sécurisation |Informer l’équipe de projet Mark 8 |

### Concevoir des compromis et des solutions alternatives

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1: configurer une source de données supplémentaire dans le Niveau de sécurité

Dans cette tâche, vous allez activer des sources de données supplémentaires pour le Niveau de sécurité afin d’obtenir plus de recommandations sur votre surface d’attaque.

1. Connectez-vous à la machine virtuelle Client 1 (LON-SC1) en tant que compte **lon-sc1\admin** . Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à <https://security.microsoft.com> et connectez-vous au Centre d’administration Microsoft 365 en tant qu’**administrateur MOD**<admin@WWLxZZZZZZ.onmicrosoft.com> (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.
3. Dans la boîte de dialogue **Rester connecté ?**, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
4. Il vous sera demandé de configurer l’authentification multifacteur, suivez les instructions.
5. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant **Jamais**, pour ne pas enregistrer les informations d’identification d’administration générale par défaut dans votre navigateur.
6. Dans le volet de navigation de gauche, sélectionnez **Paramètres**.
7. Sélectionnez **Microsoft Defender XDR**.
8. Sous Général, sélectionnez **Autorisations et rôles**.
9. Vous devrez peut-être attendre quelques minutes pour que Microsoft Defender XDR soit configuré.
10. Activez **Sources de données supplémentaires**.
11. Revenez au tableau de bord Niveau de sécurité

Vous avez activé des sources de données supplémentaires pour configurer l’accès en fonction du rôle aux recommandations de produit spécifiques.

### Tâche 2: configurer le RBAC pour le Niveau de sécurité

Dans cette tâche, vous allez vous assurer que seules les personnes sélectionnées peuvent accéder à ces informations. Vous activez le RBAC pour le Niveau de sécurité et vous le basez sur le concept d’accès au moindre privilège.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender XDR.
2. Dans le volet de navigation de gauche, sélectionnez **Paramètres**.
3. Sélectionnez **Microsoft Defender XDR**.
4. Sélectionnez **Autorisations et rôles**.
5. Sélectionnez **Accéder à Autorisations et rôles**.
6. Sélectionnez **Créer un rôle personnalisé**.
7. Nom du rôle : SecureScore Apps
8. Cliquez sur **Suivant**.
9. Cliquez sur **État de la sécurité**, sélectionnez **Sélectionner des autorisations personnalisées**, puis **Sélectionner des autorisations personnalisées**.
10. Choisissez **Niveau de sécurité (gérer)**.
11. Sélectionnez **Appliquer**.
12. Cliquez sur **Suivant**.
13. Sélectionnez **Ajouter une attribution**.
14. Nom de l’attribution : SecureScore Manager
15. Attribuez-le à **Joni Sherman**. 
16. Sous **Sources de données**, **décochez** tout sauf **Niveau de sécurité Microsoft - Sources de données supplémentaires**.
17. Sélectionnez **Ajouter**.
18. Sélectionnez **Suivant**.
19. Sélectionnez **Soumettre**.

Vous avez correctement implémenté le RBAC pour accéder aux recommandations de source de données supplémentaires pour Joni Sherman dans le Niveau de sécurité.

### Tâche 3: déléguer une action

L’équipe de projet Mark 8 de Contoso est responsable du développement ultérieur de la gestion des périphériques mobiles. Par conséquent, vous allez informer l’équipe du projet de votre recommandation en matière de sécurité.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender XDR.
2. Dans le volet de navigation de gauche, sélectionnez **Niveau de sécurité**.
3. Dans l’onglet, sélectionnez **Actions recommandées**.
4. Recherchez et sélectionnez **Vérifier que les appareils se verrouillent après une période d’inactivité afin d’empêcher les accès non autorisés**.
5. Sélectionnez **Partager**, puis, dans le menu déroulant, sélectionnez **Microsoft Teams**.
6. Dans l e champ**Équipe**, sélectionnez **Équipe de projet Mark 8** et, dans le champ **Canal**, sélectionnez **Canal Recherche et développement**.
7. Sélectionnez **Publier un message dans Teams**.

Joni Sherman et son équipe de projet Mark 8 seront avertis de l’action recommandée dans leur canal d’équipe.

### Tâche 4 : gérer les recommandations

En tant que Joni Sherman, vous avez reçu la notification Teams indiquant qu’une action spécifique pour augmenter l’état de la sécurité a été recommandée. Vous allez gérer l’action recommandée et documenter la solution.

Dans cette tâche, vous allez gérer les actions recommandées et documenter vos solutions.

1. Ouvrez une fenêtre Microsoft Edge inPrivate, accédez à <https://office.com> et connectez-vous en tant que <JoniS@WWLxZZZZZZ.onmicrosoft.com>.
2. Ouvrez Teams, puis le canal **Recherche et développement** dans **Équipe de projet Mark 8**.
3. Passez en revue le message publié à partir de l’action du Niveau de sécurité.
4. Ouvrez un autre onglet dans la fenêtre Microsoft Edge inPrivate et accédez à <https://security.microsoft.com>.
5. Dans le volet de navigation de gauche, sélectionnez **Niveau de sécurité**.
6. Sélectionnez l’onglet **Actions recommandées** pour afficher toutes les actions auxquelles vous avez accès.
7. Recherchez et sélectionnez **Vérifier que les appareils se verrouillent après une période d’inactivité afin d’empêcher les accès non autorisés**.
8. Sélectionnez **Modifier l’état et le plan d’action**.
9. Cochez **Résolu par le biais d’un tiers**.
10. Ajoutez une note **Actuellement sécurisée avec JAMF** au champ **Plan d’action**.
11. Sélectionnez **Enregistrer et fermer**.

Vous avez correctement configuré des charges de travail supplémentaires pour le Niveau de sécurité, attribué l’autorisation en fonction de l’accès au moindre privilège, et géré et délégué des actions recommandées à l’équipe des identités de Contoso Ltd.
