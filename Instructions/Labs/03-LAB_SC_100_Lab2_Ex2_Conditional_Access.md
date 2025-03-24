# Accès conditionnel

Vous avez découvert que les employés accèdent à Microsoft 365 à partir d’emplacements inconnus, même si vos stratégies d’accès conditionnel autorisent uniquement l’accès à partir d’emplacements et d’appareils spécifiques. Votre enquête a révélé que ces employés accédaient à Microsoft 365 lorsqu’ils se rendaient à leur domicile dans les transports en commun. Ce comportement est contraire aux réglementations du secteur et vous souhaitez utiliser l’évaluation continue de l’accès pour y remédier. En outre, vous souhaitez implémenter la force d’authentification que vous avez préparée dans l’exercice précédent pour sécuriser certaines applications qui gèrent les données client. 

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour répondre aux risques auxquels Contoso Ltd. est confronté.

### Approche de conception

La première étape consiste à analyser les exigences en fonction du problème décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Restreindre l’accès à partir d’emplacements non sécurisés/inconnus
- Exiger une authentification forte pour les applications contenant des informations sensibles

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Microsoft Entra ID propose des solutions pour gérer et restreindre l’accès utilisateur à l’aide des stratégies d’accès conditionnel d’Entra ID. Examinez les contrôles et les stratégies actuels. Utilisez le portail Entra ID pour passer en revue les configurations et stratégies actuelles et déterminer si des ajustements sont nécessaires ou si de nouvelles stratégies doivent être implémentées.

La troisième phase consiste à élaborer le concept de la solution. Après enquête, il est évident qu’il n’y a pas encore de réseau de confiance configuré et qu’aucune des stratégies actuelles ne répond aux exigences définies. Par conséquent, un nouvel ensemble de stratégies d’accès conditionnel est essentiel. 

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Restreindre l’accès à partir d’emplacements non sécurisés/inconnus|Stratégie d’accès conditionnel Entra ID|Définir les réseaux actuels de l’entreprise en tant que réseau approuvé et restreindre l’accès aux appareils au sein de ce réseau|
|Exiger une authentification forte pour les applications contenant des informations sensibles|Stratégie d’accès conditionnel Entra ID|Créer une nouvelle stratégie d’accès conditionnel ciblant les applications sensibles utilisant la force d’authentification renforcée qui vient d’être créée et qui exclut les méthodes d’authentification non sécurisées telles que les SMS et la voix.|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 - Créer un réseau de confiance

Dans cette tâche, vous allez créer un emplacement nommé à l’aide de l’adresse IP externe de votre machine virtuelle pour définir un réseau de confiance que vous pouvez utiliser dans une stratégie d’accès conditionnel dans les tâches suivantes. Vous utiliserez cette adresse, car votre ordinateur se trouve dans votre réseau d’entreprise.

1. Connectez-vous à la machine virtuelle Client 1 (LON-Sc1) en tant que compte **lon-sc1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Ouvrez une fenêtre **PowerShell** en sélectionnant le menu Démarrer avec le bouton droit de la souris, puis sélectionnez **Terminal**.
1. Entrez la cmdlet suivante pour vérifier votre adresse IP externe actuelle : `Invoke-RestMethod -Uri "http://ifconfig.me/ip"`
1. Notez l’adresse IP renvoyée par powershell.
1. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **`https://entra.microsoft.com`** et connectez-vous au portail Entra ID en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.
1. Si vous êtes invité à configurer une authentification multifacteur, suivez les instructions.
1. Dans la boîte de dialogue Rester connecté ?, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
1. Fermez la boîte de dialogue Enregistrer le mot de passe en sélectionnant **Pas maintenant** afin de ne pas enregistrer les informations d’identification de l’administrateur général ou l’administratrice générale par défaut dans votre navigateur.
1. Dans le volet de navigation de gauche, accédez à **Protection** > **Accès conditionnel** > **Emplacements nommés**.
1. Sélectionnez **+ Emplacement des plages d’adresses IP**.
1. Entrez le nom **Réseau Contoso de confiance**.
1. Sélectionnez **Marquer comme emplacement approuvé**.
1. Sélectionnez **+** pour ajouter l’adresse IP que vous avez notée à **l’étape 4**.
1. L’entrée doit ressembler à ``168.245.***.***/32`` (*** peut être différente en fonction de votre fournisseur d’hébergement de labo).
1. Sélectionnez **Ajouter**.
1. Sélectionnez **Créer**.

Vous avez défini l’adresse IP externe de votre entreprise, nommé et approuvé l’emplacement que vous pouvez utiliser pour restreindre l’accès en dehors du réseau de l’entreprise.

### Tâche 2 : créer une stratégie d’accès conditionnel avec une portée limitée

Vous avez réussi à créer un réseau approuvé. Vous allez maintenant l’utiliser pour créer la stratégie d’accès conditionnel afin de restreindre l’accès en dehors du réseau d’entreprise avec une portée limitée à votre utilisateur personnel. Cela va vous permettre de tester et d’empêcher le verrouillage des comptes de l’entreprise dans Entra ID.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
2. Dans le volet de navigation de gauche, accédez à **Protection** > **Accès conditionnel** > **Stratégies**.
3. Sélectionnez **+ Nouvelle stratégie**.
4. Entrez le nom **Bloquer l’accès en dehors du réseau approuvé**.
5. Sélectionnez **0 utilisateur et groupe sélectionné**.
6. Sous **Inclure**, sélectionnez **Sélectionner des utilisateurs et des groupes**, puis cliquez sur **Utilisateurs et groupes**.
7. Sélectionnez **Allan Deyoung** comme seul utilisateur de test pour la stratégie.
8. Sélectionnez **Aucune ressource cible sélectionnée** et, sous **Inclure**, sélectionnez **Toutes les applications cloud**.
9. Sélectionnez **0 conditions sélectionnées** et, sous **Emplacements**, sélectionnez **Non configuré**.
10. Sélectionnez **Oui** pour configurer la condition d’emplacement.
11. Sous **Inclure**, sélectionnez **Tous les emplacements**.
12. Sous **Exclure**, sélectionnez **Tous les emplacements approuvés**.
13. Sous **Accorder**, sélectionnez **0 contrôles sélectionnés** et passez de **Accorder l’accès** à **Bloquer l’accès**, puis choisissez **Sélectionner** en bas de la page.
14. Sous **Session**, sélectionnez **0 contrôles sélectionnés**.
15. Activez **Personnaliser l’évaluation continue de l’accès** et sélectionnez **Appliquer strictement les stratégies d’emplacement (préversion)**, puis **Sélectionner** en bas pour confirmer.
16. Sous **Activer la stratégie**, sélectionnez **Activé**, puis **Créer**.

Vous avez créé et activé votre stratégie d’accès conditionnel pour restreindre l’accès en dehors des réseaux approuvés qui affectent uniquement votre propre compte d’utilisateur de test.

### Tâche 3 : tester la stratégie configurée

Étant donné que vous avez créé une stratégie d’accès conditionnel limitant l’accès à toutes les applications cloud de votre entreprise, vous devez vérifier que l’accès est toujours possible.

>[! ALERTE] Cette tâche est considérablement abrégée à des fins d’illustration !
Dans un scénario réel, vous effectuez une période de test plus longue avec un groupe plus grand et plus représentatif pour vous assurer qu’aucun incident imprévisible ne fausse le résultat.

1. Ouvrez une nouvelle fenêtre **InPrivate** dans votre navigateur **Microsoft Edge** en sélectionnant son icône dans la barre des tâches avec le bouton droit de la souris, puis sélectionnez **Nouvelle fenêtre InPrivate**.
1. Sélectionnez la barre d’adresse, accédez à **`https://portal.microsoft.com`** et connectez-vous au portail M365 en tant qu’**Allan Deyoung**alland@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Dans la boîte de dialogue Rester connecté ?, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
1. La connexion a réussi, vous pouvez donc fermer la fenêtre **InPrivate**.
1. Revenez à votre fenêtre de navigateur Edge dans laquelle vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
1. Dans le volet de navigation de gauche, accédez à **Protection** > **Accès conditionnel** > **Surveillance** > **Journaux de connexion**.
1. Sélectionnez **Ajouter des filtres** et filtrer par l’**utilisateur** d’**Allan Deyoung**.
1. Sélectionnez la dernière entrée de journal d’**Allan Deyoung**.
1. Sous l’onglet **Accès conditionnel**, sélectionnez **Bloquer l’accès en dehors du réseau approuvé**.
1. Sélectionnez l’attribution **Utilisateur** et vous devriez voir qu’elle **correspond** par **Attribution directe**.
1. Sélectionnez l’attribution **Application** et vous devriez voir qu’elle **correspond** par **Toutes les applications incluses**.
1. Vous devriez également voir que la condition **Emplacement** **ne correspond pas**, car elle se trouve dans le réseau approuvé exclu.
Si vous avez essayé de vous connecter à partir d’un réseau avec une autre adresse IP externe, cette condition correspond et bloque la tentative de connexion.
1. Fermez **Détails de la stratégie d’accès conditionnel** et **Détails de l’activité : connexions**.

Vous avez testé et vérifié l’accès à toutes les applications cloud à partir du réseau de l’entreprise. Vous avez également vérifié les journaux de connexion pour vous assurer que la stratégie fonctionne comme prévu et utilise les attributions et conditions appropriées pour restreindre l’accès à vos applications cloud à partir de l’extérieur du réseau de l’entreprise.

### Tâche 4 : déployer la stratégie à l’échelle de l’entreprise

Comme le test a réussi dans la tâche précédente, vous pouvez activer la stratégie pour l’ensemble de l’entreprise. Pour ce faire, vous allez modifier la portée utilisateur de la stratégie existante.

>[! ALERTE] Les actions implémentées dans cette tâche peuvent entraîner un verrouillage de compte !
Assurez-vous que vous disposez d’au moins un compte Administrateur d’urgence exclu de cette stratégie dans un scénario de production réel. 

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
2. Dans le volet de navigation de gauche, accédez à **Protection** > **Accès conditionnel** > **Stratégies**.
3. Sélectionnez la stratégie **Bloquer l’accès en dehors du réseau approuvé**.
4. Sous Utilisateurs, sélectionnez **Utilisateurs spécifiques inclus**.
5. Sélectionnez **Tous les utilisateurs**.
6. Dans l’avertissement qui s’affiche en bas de la fenêtre, sélectionnez **Exclure l’utilisateur actuel, admin@WWLxZZZZZZ.onmicrosoft.com, dans cette stratégie**.
7. Cliquez sur **Enregistrer**.

Vous avez configuré une stratégie d’accès conditionnel active qui empêche les utilisateurs et les utilisatrices de se connecter en dehors du réseau approuvé que vous avez défini comme adresse IP externe de l’entreprise. Vous avez effectué un test à l’aide d’une portée utilisateur limitée pour garantir que toutes les applications cloud restent accessibles. Enfin, vous avez déployé la stratégie d’accès conditionnel pour tous les utilisateurs et utilisatrices.

Vous avez réussi à restreindre l’accès à partir de l’extérieur du réseau approuvé.

### Tâche 5 : appliquer l’authentification multifacteur pour Salesforce

Dans cette tâche, vous créez une stratégie d’accès conditionnel pour appliquer l’authentification renforcée que vous avez créée dans l’exercice précédent lors de la connexion à Salesforce. 

>[!IMPORTANT] Important : cette tâche ignore la phase de test. Dans un scénario réel, vous allez d’abord tester avec une portée utilisateur limitée comme indiqué dans les tâches précédentes et effectuer un déploiement complet après une phase de test réussie.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
2. Dans le volet de navigation de gauche, accédez à **Protection** > **Accès conditionnel** > **Stratégies**.
3. Sélectionnez **+ Nouvelle stratégie**.
4. Entrez le nom **Authentification renforcée Salesforce**.
5. Sélectionnez **0 utilisateur et groupe sélectionné**.
6. Sous **Inclure**, sélectionnez **Sélectionner des utilisateurs et des groupes**, puis cliquez sur **Utilisateurs et groupes**.
7. Sélectionnez **Alex Wilber** dans Sales comme unique utilisateur de test pour la stratégie.
8. Sélectionnez **Aucune ressource cible sélectionnée**, puis, sous **Inclure**, sélectionnez **Sélectionner des applications**.
9. Sous **Sélectionner**, sélectionnez **Aucune** et recherchez **Salesforce**.
10. Confimez votre choix avec le bouton **Sélectionner**.
11. Sous **Accorder**, sélectionnez **0 contrôles sélectionnés** et activez **Appliquer l’authentification renforcée**.
12. Sélectionnez votre authentification renforcée personnalisée **MFA renforcée** et confirmez avec le bouton **Sélectionner**.
13. Définissez maintenant la stratégie sur **Activée** à l’aide de la barre de contrôle en bas, puis sélectionnez **Créer**.
14. Après une phase de test réussie avec votre portée d’utilisateur limitée, sélectionnez **Authentification renforcée Salesforce**.
15. Sous Utilisateurs, sélectionnez **Utilisateurs spécifiques inclus**.
16. Sélectionnez **Tous les utilisateurs**.
17. Cliquez sur **Enregistrer**.

Vous avez créé une stratégie d’accès conditionnel pour appliquer votre stratégie d’authentification renforcée à Salesforce en excluant le protocole OTP SMS et ainsi empêcher les attaques via l’interception de SMS.
