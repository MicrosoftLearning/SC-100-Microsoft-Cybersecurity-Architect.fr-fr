# Labo 2 - Exercice 1 - Configurer Entra ID

Vous êtes Allan Deyoung, le nouveau spécialiste de la sécurité informatique de Contoso Ltd. Comme l’entreprise a récemment acquis Tailwind Traders, vous avez examiné votre locataire Entra ID et décidé d’appliquer de nouvelles exigences de sécurité. Votre tâche consiste à gérer les tâches et à implémenter des stratégies pour répondre aux exigences qui accompagnent l’acquisition. 

Vous avez examiné les applications d’entreprise et noté que certains utilisateurs et certaines utilisatrices ont fourni des autorisations à une application tierce pour accéder à leurs données de boîte aux lettres. Il s’agit d’un risque potentiel de perte de données provenant des correspondances par e-mail. Par conséquent, vous souhaitez limiter ce comportement, mais autoriser les utilisateurs et utilisatrices à se connecter et à partager des ID de connexion aux sites web que Microsoft a validés. Vous souhaitez également autoriser les utilisateurs et utilisatrices à demander un accès spécifique aux nouveaux produits SaaS à l’aide de leur identité Entra ID. 

Étant donné qu’une organisation partenaire a récemment été attaquée par l’interception de SMS, vous souhaitez appliquer l’assurance d’authentification après NIST. Pour ce faire, vous allez créer une stratégie de renforcement de l’authentification pour désactiver le mot de passe à usage unique par SMS et restreindre l’utilisation des méthodes d’authentification AAL1 dans votre organisation. Vous allez créer cette configuration dans le portail Entra ID.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour répondre aux risques auxquels Contoso Ltd. est confronté.

### Approche de conception

La première étape consiste à analyser les exigences en fonction du problème décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Restreindre l’accès non contrôlé à partir d’applications tierces
- Autoriser les utilisateurs et les utilisatrices à partager des ID de connexion à des services validés
- Autoriser les utilisateurs et les utilisatrices à demander l’accès aux produits SaaS
- Renforcer l’authentification

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Microsoft Entra ID propose des solutions pour gérer et restreindre l’accès des utilisateurs et utilisatrices et de l’application cloud à l’aide de stratégies Entra ID. Examinez les contrôles et les stratégies actuels. Utilisez le portail Entra ID pour passer en revue les configurations et stratégies actuelles et déterminer si des ajustements sont nécessaires ou si de nouvelles stratégies doivent être implémentées.

La troisième phase consiste à élaborer le concept de la solution. L’examen des stratégies actuelles permet de conclure qu’aucune d’entre elles ne répond aux exigences définies. Par conséquent, il est essentiel de procéder à des ajustements de la configuration Entra ID. 

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Bloquer l’accès non contrôlé à partir d’applications tierces|Stratégie d’application Entra ID|Restreindre le consentement de l’utilisateur ou l’utilisatrice à des autorisations classées comme ayant un « faible impact », pour les applications d’éditeurs vérifiés ou les applications enregistrées dans cette organisation.|
|Autoriser les utilisateurs et les utilisatrices à partager des ID de connexion à des services validés|Stratégie d’application Entra ID|Restreindre le consentement de l’utilisateur ou l’utilisatrice à des autorisations classées comme ayant un « faible impact », pour les applications d’éditeurs vérifiés ou les applications enregistrées dans cette organisation.|
|Autoriser les utilisateurs et les utilisatrices à demander l’accès aux produits SaaS|Stratégie d’application Entra ID|Définir les utilisateurs et utilisatrices habilités à approuver les applications dont l’utilisation est sûre|
|Restreindre l’utilisation des méthodes d’authentification non sécurisées|Méthodes d’authentification Entra ID|Créer un système de renforcement de l’authentification qui exclut les méthodes SMS et vocale|

## Partie 2 : implémenter la solution (facultatif)

**Remarque :** ces étapes de labo doivent être exécutées sur le profil de labo M365.

### Tâche 1 : restreindre l’utilisation d’applications tierces aux services vérifiés Par Microsoft

Dans cette tâche, vous limiterez le niveau d’accès qu’un utilisateur ou une utilisatrice peut accorder aux applications. Vous allez également ajouter les fonctionnalités permettant aux utilisateurs et utilisatrices de demander l’accès qu’ils ne peuvent pas s’accorder eux-mêmes. 

1. Connectez-vous à la machine virtuelle Client 1 (LON-Sc1) en tant que compte **lon-sc1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **https://entra.microsoft.com** et connectez-vous au portail Entra ID en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit vous être fourni par votre fournisseur d’hébergement de labo.
3. Dans la boîte de dialogue **Rester connecté ?**, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
4. Il vous sera demandé de configurer l’authentification multifacteur, suivez les instructions.
5. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant **Jamais**, pour ne pas enregistrer les informations d’identification d’administration générale par défaut dans votre navigateur.
6. Dans le volet de navigation de gauche, accédez à **Identité** > **Applications** > **Applications d’entreprise** > **Sécurité** > **Consentement et autorisations**.
7. Accédez à **Classifications d’autorisations**.
8. Entra suggère les autorisations les plus utilisées pour les autorisations **à faible risque**.
9. Vérifiez toutes ces autorisations et sélectionnez **Oui, ajouter les autorisations sélectionnées** pour les classer comme étant **à faible risque** dans votre locataire Entra ID.
10. Accédez à **Paramètres de consentement de l’utilisateur**.
11. Sous **Consentement de l’utilisateur pour les applications**, sélectionnez l’option recommandée **Autoriser le consentement de l’utilisateur pour les applications d’éditeurs vérifiés, pour les autorisations sélectionnées** permettant aux utilisateurs et utilisatrices de donner leur consentement aux autorisations **à faible impact** que vous avez définies à l’étape 8 aux applications d’éditeurs vérifiés.
12. Sous **Consentement du propriétaire du groupe pour les applications accédant aux données**, sélectionnez **Ne pas autoriser le consentement du propriétaire du groupe**. Cela limite le consentement du propriétaire du groupe aux utilisateurs et utilisatrices qui ont déjà le rôle éligible ou activé pour donner leur consentement à d’autres autorisations que celles définies comme **à faible risque**.
13. Cliquez sur **Enregistrer**.
14. Accédez à **Paramètres de consentement administrateur** et activez les demandes de consentement administrateur en sélectionnant **Oui**.
15. Sélectionnez **+ Ajouter des utilisateurs** pour ajouter **Lidia Holloway** et **l’administrateur MOD** en tant qu’utilisateurs capables de passer en revue les demandes de consentement administrateur.
16. Sélectionnez **Enregistrer** dans la fenêtre **Paramètres de consentement administrateur**.

Vous avez configuré les paramètres de consentement de l’application limitant l’accès que chaque utilisateur et utilisatrices peut accorder aux applications. Les utilisateurs et les utilisatrices peuvent toujours demander le consentement aux autorisations aux applications et l’équipe d’administration de l’application peut les approuver après avoir évalué le besoin et le risque de l’application en question. 

### Tâche 2 - Créer une authentification renforcée

Dans cette tâche, vous allez utiliser le portail Entra ID pour créer une authentification renforcée propre pour restreindre l’utilisation du protocole OTP SMS au sein de votre organisation. 

1. Vous devriez toujours vous trouver dans le portail Entra ID **https://entra.microsoft.com**.
2. Dans le volet de navigation de gauche, accédez à **Protection** > **Méthodes d’authentification** > **Authentifications renforcées**.
3. Sélectionnez **Nouvelle authentification renforcée**.
4. Entrez le nom **MFA renforcée**.
5. Cochez **MFA résistante au hammeçonnage**, **MFA sans mot de passe** et **Authentification multifacteur**.
6. Sous Authentification multifacteur, décochez les éléments suivants :
   - **Passe d’accès temporaire (multi-usage)**
   - **Mot de passe + SMS**
   - **Mot de passe + vocal**
   - **Facteur unique fédéré + SMS**
   - **Facteur unique fédéré + vocal**.
7. Cliquez sur **Suivant**.
8. Vérifiez que vous n’avez laissé aucun des facteurs ci-dessus dans l’authentification renforcée.
9.  Sélectionnez **Créer**.

Vous avez créé une authentification renforcée qui limite l’utilisation du protocole OTP SMS comme facteur d’authentification.
