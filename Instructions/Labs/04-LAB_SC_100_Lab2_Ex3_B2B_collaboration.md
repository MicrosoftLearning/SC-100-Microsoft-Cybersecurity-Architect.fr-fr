# Synchronisation entre clients

Contoso a récemment acquis Tailwind Traders et il est difficile de déterminer quels invités sont des clients ou des partenaires, et quels sont les employés de l’entreprise acquise. Votre tâche consiste à fournir une liste d’adresses commune initiale de Tailwind Traders à Contoso. En outre, votre client doit uniquement autoriser l’ajout de noms de domaine connus en tant qu’invités à Entra ID. Vous souhaitez limiter les personnes pouvant inviter des invités à l’organisation aux utilisateurs internes uniquement. Vous limiterez l’accès externe à un seul domaine. Vous allez également créer une collaboration B2B et une synchronisation entre clients entre Tailwind Traders et Contoso.

En tant qu’architecte en cybersécurité, vous devez vous assurer que toutes les exigences sont remplies et implémenter les modifications nécessaires dans Entra ID pour appliquer les principes de Confiance Zéro. Dans cet exercice, vous allez collaborer avec un partenaire de labo pour créer une synchronisation entre clients.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour répondre aux exigences de Contoso Ltd. et Tailwind Traders.

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Synchroniser les utilisateurs des deux entreprises
- Permettre d’identifier les utilisateurs externes
- Restreindre les droits d’invitation aux employés internes uniquement 
- Restreindre les accès externes aux domaines approuvés de l’entreprise

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Microsoft Entra ID propose des solutions pour permettre la collaboration externe. Examinez les contrôles et les stratégies actuels. Utilisez le portail Entra ID pour passer en revue les configurations et stratégies actuelles et déterminer quels ajustements doivent être implémentés pour répondre aux exigences de l’intégration.

La troisième phase consiste à élaborer le concept de la solution. Après enquête, il est évident que la synchronisation entre clients est le meilleur moyen de permettre une collaboration répondant à toutes les exigences.  

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Restreindre les droits d’invitation aux employés internes uniquement|Paramètres de collaboration externe|Limiter les droits d’invitation aux membres du client et aux rôles d’invitation spécifiques aux administrateurs|
|Bloquer les invitations de tous les domaines sauf les domaines de confiance|Paramètres de collaboration externe|Créer une liste d’autorisation d’invitations incluant uniquement les domaines approuvés|
|Synchroniser les utilisateurs des deux entreprises|Synchronisation entre clients dans Entra ID|Établir une confiance d’accès entre les deux clients d’Entra ID et créer une configuration qui synchronise les utilisateurs avec l’autre client|
|Permettre d’identifier les utilisateurs externes|Mappage des attributs entre clients|Modifier l’attribut displayName de chaque utilisateur synchronisé en créant une expression personnalisée à l’aide de la fonction de mappage d’attributs de la configuration de synchronisation entre clients|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 - Formation d’une équipe et préparatifs

Dans cette tâche, vous allez vérifier les conditions préalables d’une synchronisation entre clients et collaborer avec un partenaire de labo.

1. Connectez-vous à la machine virtuelle Client 1 (LON-Sc1) en tant que compte **lon-sc1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **`https://entra.microsoft.com`** et connectez-vous au portail Entra ID en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.
1. Si vous êtes invité à configurer une authentification multifacteur, suivez les instructions.
1. Dans la boîte de dialogue **Rester connecté ?**, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
1. Fermez la boîte de dialogue Enregistrer le mot de passe en sélectionnant **Pas maintenant** afin de ne pas enregistrer les informations d’identification de l’administrateur général ou l’administratrice générale par défaut dans votre navigateur.
1. Dans le volet de navigation de gauche, accédez à **Identité** > **Vue d’ensemble**.
1. Notez l’**ID de client** et le **domaine principal** fournis sous l’onglet **Vue d’ensemble**.
1. Échangez votre **ID de client** et votre **domaine principal** avec votre partenaire de labo.

Vous devez avoir une idée de la topologie que vous souhaitez utiliser, des utilisateurs qui seront concernés par le premier test de synchronisation et de la manière dont vous souhaitez les associer au client Entra ID de Contoso.

### Tâche 2 - Configurer l’accès entre clients

Maintenant que vous avez préparé les informations nécessaires pour mettre en œuvre la synchronisation entre clients, vous allez effectuer les étapes nécessaires pour que votre client accède au client de votre partenaire et vice-versa.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
1. Dans la barre de navigation de gauche, accédez à **Identité** > **Identités externes** > **Paramètres d’accès interlocataire**.
1. Sélectionnez l’onglet **Paramètres organisationnels**, puis **Ajouter une organisation**.
1. Renseignez l’**ID de client ou le nom de domaine** avec l’ID de client fourni par votre partenaire de labo, puis sélectionnez **Ajouter**.
1. Sous **Accès entrant** pour Contoso, sélectionnez **Hérité par défaut** pour accéder aux paramètres de synchronisation entre clients pour ce client spécifique.
1. Sous **Paramètres d’approbation**, activez **Accepter automatiquement les invitations avec le locataire Contoso**.
1. Cliquez sur **Enregistrer**.
1. Sous **Synchronisation entre clients**, activez **Autoriser les utilisateurs à se synchroniser avec ce client**.
1. Sélectionnez **Enregistrer** et fermez la boîte de dialogue à l’aide du **X** dans le coin supérieur droit.
1. Sous **Accès sortant** pour Contoso, sélectionnez **Hérité de la valeur par défaut** pour accéder aux paramètres de synchronisation entre clients pour ce client spécifique.
1. Sous **Paramètres d’approbation**, activez **Accepter automatiquement les invitations avec le locataire Contoso**.
1. Sélectionnez **Enregistrer** et fermez la boîte de dialogue à l’aide du **X** dans le coin supérieur droit.

Vous avez permis à votre client de se synchroniser avec le client de votre partenaire sans que les utilisateurs aient besoin d’accepter leurs invitations manuellement. 

### Tâche 3 - Restreindre l’accès externe

Dans cette tâche, vous limiterez la possibilité d’inviter de nouveaux utilisateurs à votre organisation en contrôlant le nombre d’utilisateurs autorisés à envoyer des invitations. Vous limiterez l’étendue des domaines qui peuvent être invités dans le domaine locataire de votre partenaire.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
1. Dans le volet de navigation de gauche, accédez à **Identité** > **Identités externes** > **Paramètres de collaboration externes**.
1. Sous **Paramètres d’invitation d’invité**, sélectionnez **Les utilisateurs membres et les utilisateurs affectés à des rôles d’administrateur spécifiques peuvent inviter des utilisateurs invités, y compris des invités disposant d’autorisations de membre**.
1. Sous **Restrictions de collaboration**, sélectionnez **Autoriser les invitations uniquement vers les domaines spécifiés**.
1. Ajoutez le domaine de votre partenaire de labo **WWLxZZZZZZ.onmicrosoft.com** (où ZZZZZZ est l’ID de locataire unique de votre partenaire de labo fourni par votre fournisseur d’hébergement de labo).
1. Cliquez sur **Enregistrer**.

Vous avez maintenant limité le nombre de personnes qui peuvent inviter et qui peuvent être invitées dans votre locataire.

### Tâche 4 - Créer une configuration

Dans cette tâche, vous allez créer une configuration de base et tester la connexion à l’autre locataire.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
1. Dans le volet de navigation de gauche, accédez à **Identité** > **Identités externes** > **Synchronisation entre clients** > **Configurations**.
1. Créer une **Nouvelle configuration**.
1. Entrez le nom **Synchronisation entre clients de Contoso**, puis sélectionnez **Créer**.
1. Sous **Approvisionnement**, définissez le **Mode Approvisionnement** sur **Automatique**.
1. Dans la zone **ID de locataire**, entrez l’ID de locataire de votre partenaire que vous avez noté dans la tâche 1.
1. Sélectionnez **Test Connection** (Tester la connexion).
1. Cliquez sur **Enregistrer**.

Si vous avez configuré correctement les paramètres d’accès, vous devriez voir un message indiquant que les informations d’identification fournies sont autorisées à activer l’approvisionnement. Si le test de connexion échoue, vérifiez si votre partenaire a entré le domaine approprié à la tâche 3 et configuré la synchronisation entre clients, comme décrit à la tâche 2.

### Tâche 5 - Définir l’étendue des utilisateurs

Dans cette tâche, vous définirez qui est concerné par la première synchronisation.

1. Vous devriez toujours être connecté au portail Entra ID **https://entra.microsoft.com** dans les paramètres d’approvisionnement de la configuration que vous venez de créer. Si ce n’est pas le cas, suivez ces trois étapes pour y revenir :
   1. Dans le volet de navigation de gauche, accédez à **Identité** > **Identités externes** > **Synchronisation entre clients** > **Configurations**.
   1. Sélectionnez **Synchronisation entre clients Contoso**.
   1. Accédez à **Approvisionnement**.
1. Développez la section **Paramètres**.
1. Vérifiez que la liste déroulante Étendue est définie sur **Synchroniser uniquement les utilisateurs et les groupes affectés**.
1. Si vous avez dû modifier cette configuration, sélectionnez **Enregistrer**.
1. Sélectionnez **Utilisateurs et groupes** dans le volet de navigation.
1. Sélectionner **Ajouter un utilisateur/groupe**.
1. Sur la page **Ajouter une attribution**, sélectionnez **Aucune sélection**.
1. Recherchez **Juridique** et mettez en surbrillance **Équipe juridique** en utilisant la case à cocher, puis sélectionnez **Sélectionner**.
1. Sélectionnez **Attribuer** pour ajouter l’équipe composée de deux utilisateurs ou utilisatrices à la portée de la synchronisation.

Vous avez défini votre première portée d’utilisateurs et utilisatrices pour la synchronisation avec le locataire de votre partenaire.

### Tâche 6 : vérifier les mappages d’attributs

Dans cette tâche, vous allez examiner les mappages d’attributs et vous assurer que les utilisateurs synchronisés s’affichent dans la liste d’adresses globale de Contoso.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com** dans les paramètres **Utilisateurs et groupes** de la configuration de synchronisation entre clients. Si ce n’est pas le cas, suivez ces deux étapes pour revenir à la page de configuration :
   1. Dans le volet de navigation de gauche, accédez à **Identité** > **Identités externes** > **Synchronisation entre clients** > **Configurations**.
   1. Sélectionnez **Synchronisation entre clients Contoso**.
1. Accédez à **Approvisionnement** et développez la section **Mappages**.
1. Sélectionnez **Provisionner les utilisateurs de Microsoft Entra ID**.
1. Sous l’attribut **showInAddressList**, sélectionnez Modifier.
1. Vérifiez que son type de mappage est défini sur **Constant** et que sa valeur est définie sur **true**.
1. Sélectionnez **OK**.
1. Sous l’attribut **displayName**, sélectionnez **Modifier**.
1. Redéfinissez le type de mappage sur **Expression**.
1. Supprimez l’expression préexistante.
1. Sélectionnez **Utiliser le générateur d’expressions**.
1. Sélectionnez la fonction **Append**.
1. Dans le champ **Sélectionner un attribut**, sélectionnez l’attribut **[displayName]** dans la liste déroulante.
1. Dans le champ **Entrer un suffixe**, entrez **' (Contoso)'**, y compris l’espace devant la parenthèse, mais sans les guillemets.
1. Sélectionnez **Ajouter l’expression**. Votre expression à droite doit ressembler à `Append([displayName], " (Contoso)")`
1. Vous pouvez tester votre expression en sélectionnant un utilisateur ou une utilisatrice.
1. Sélectionnez **Appliquer l’expression**, puis **OK** pour quitter la boîte de dialogue Modifier.
1. Cliquez sur **Enregistrer**.
1. Fermez la page Mappage d’attributs en cliquant sur le **X** en haut à droite.

Vous avez fait en sorte que tous les utilisateurs synchronisés s’affichent dans la liste d’adresses globale de l’autre locataire. Vous avez également ajouté une expression (Contoso) au nom complet de chaque utilisateur synchronisé au sein de l’autre locataire.

### Tâche 7 : activer l’approvisionnement et tester avec votre partenaire de labo

Dans cette tâche, vous allez activer l’approvisionnement et tester si vos utilisateurs et utilisatrices apparaissent dans l’autre locataire de la façon qui vous convient. Étant donné que l’approvisionnement automatique peut prendre un certain temps, nous déclencherons un approvisionnement manuel.

1. Vous devrer toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com** dans les paramètres Approvisionnement de la configuration de synchronisation entre clients. Si ce n’est pas le cas, suivez ces deux étapes pour revenir à la page de configuration :
   1. Dans le volet de navigation de gauche, accédez à **Identité** > **Identités externes** > **Synchronisation entre clients** > **Configurations**.
   1. Sélectionnez **Synchronisation entre clients Contoso**.
1. Accédez à **Approvisionner à la demande**.
1. Recherchez **`Grady Archie`** en tant que membre de l’**équipe juridique** concernée.
1. Sélectionnez **Approvisionner**.
    - Vous recevrez une confirmation une fois l’approvisionnement terminé.
1. Fermez la page Effectuer une acction en cliquant sur le **X** en haut à droite.

Vous venez d’approvisionner votre premier utilisateur ou votre première utilisatrice manuellement. Lorsque vous consulterez la liste des utilisateurs et utilisatrices de votre locataire partenaire, vous verrez s’afficher Grady Archie (Contoso).

### Tâche 8 : déployer la synchronisation complète

Maintenant que le test de la première attribution d’utilisateurs a réussi, vous allez approvisionner le reste de votre liste d’utilisateurs et utilisatrices sur l’autre locataire.

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com** sur la page **Approvisionner à la demande** de la configuration de synchronisation entre clients. Si ce n’est pas le cas, suivez ces deux étapes pour revenir à la page de configuration :
   1. Dans le volet de navigation de gauche, accédez à **Identité** > **Identités externes** > **Synchronisation entre clients** > **Configurations**.
   1. Sélectionnez **Synchronisation entre clients Contoso**.
1. Sélectionnez **Utilisateurs et groupes**.
1. Sélectionner **Ajouter un utilisateur/groupe**.
1. Sur la page **Ajouter une attribution**, sélectionnez **Aucune sélection**.
1. Sélectionnez le groupe **Tous les employés**, car il s’agit du groupe contenant **tous les employés de Contoso**.
1. Confirmez votre sélection.
1. Sélectionnez **Attribuer**.

Vous avez créé une synchronisation entre clients entre votre locataire et un autre. Vous devriez être en mesure d’adapter tout ce que vous avez fait dans votre locataire de démonstration au système de production de Tailwind Traders et les aider à s’intégrer à Contoso.
