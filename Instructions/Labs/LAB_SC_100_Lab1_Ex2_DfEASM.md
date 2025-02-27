# Labo 1 - Exercice 2 - Gestion de la surface d’attaque externe

## Vue d’ensemble de l’exercice

Contoso vise à améliorer sa posture de cybersécurité en identifiant et en gérant sa surface d’attaque externe. Cette surface inclut des ressources hébergées sur différents fournisseurs de cloud. Pour atteindre cet objectif, Contoso souhaite intégrer ses données de surface d’attaque à Sentinel, sa solution SIEM native Cloud. Cette intégration améliore ses fonctionnalités de surveillance de la sécurité et de réponse aux incidents. 

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept permettant d’obtenir une vue d’ensemble de vos ressources tournées vers l’extérieur et de leur surface d’attaque.

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Les ressources tournées vers l’extérieur de Contoso doivent être surveillées et sécurisées
- Découvrir toutes les ressources associées à Contoso
- Intégrer des données à la solution SIEM de Contoso.
- Les ressources doivent être gérées et étiquetées

La deuxième étape consiste à étudier l’environnement actuel de Contoso Ltd.. Microsoft Defender EASM (External Attack Surface Management) découvre et mappe en permanence la surface d’attaque numérique pour fournir une vue externe de l’infrastructure en ligne d’une organisation. Il identifie les ressources exposées, hiérarchise les risques et étend la vulnérabilité et le contrôle d’exposition au-delà du pare-feu.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Les ressources tournées vers l’extérieur de Contoso doivent être surveillées et sécurisées| Defender EASM | Créer une ressource Microsoft Defender EASM|
|Découvrir toutes les ressources associées à Contoso | Defender EASM |Créer un travail de découverte sur les ressources de Contoso  |
|Intégrer des données à la solution SIEM de Contoso |Defender EASM, espace de travail Log Analytics | Connecter l’espace de travail Log Analytics à Defender EASM |
|Les ressources doivent être gérées et étiquetées | Defender EASM | Gérer les ressources et balises facturables |


## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 - Configurer Defender EASM

Dans cette tâche, vous allez créer un espace de travail Defender EASM.

1. Connectez-vous à la machine virtuelle Client 1 (LON-Sc1) en tant que compte **lon-sc1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **<https://portal.azure.com>** et connectez-vous au portail Azure en tant qu’utilisateur <user1-ZZZZZZZ@LODSUATMCA.onmicrosoft.com>. Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.
3. Dans la boîte de dialogue Rester connecté ?, cochez la case Ne plus afficher, puis sélectionnez Non.
4. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant **Jamais**, pour ne pas enregistrer les informations d’identification d’administration générale par défaut dans votre navigateur.
5. Dans la zone de recherche supérieure, recherchez **Microsoft Defender EASM**.
6. Sélectionnez **Créer**.
7. Dans Créer une ressource Microsoft Defender EASM, sélectionnez le groupe de ressources **rg_eastus_soc** existant.
8. Dans les détails de l’instance, entrez le nom **EASM** et sélectionnez **USA Est** comme région.
9. Sélectionnez **Vérifier & créer**.
10. Sélectionnez **Créer**.

Vous avez correctement créé l’espace de travail Defender EASM.

### Tâche 2 - Créer une découverte

Dans cette tâche, vous allez créer une découverte sur les ressources Contoso Ltd. exposées. Une fois que vous avez créé une instance, vous devez la remplir avec des données réelles. Vous allez donc créer une découverte.

1. Vous devriez toujours vous trouver dans le Portail Azure **<https://portal.azure.com>**.
2. Dans la barre de recherche en haut, recherchez et ouvrez **Microsoft Defender EASM**.
3. Sélectionnez l’espace de travail **EASM** que vous avez créé à la tâche précédente.
4. Recherchez **Contoso** dans le champ de recherche **Rechercher une organisation**.
5. Sélectionnez **Contoso Ltd.**.
6. Sélectionnez **Démarrer la découverte de la surface d’attaque**.

Vous avez créé la découverte de la surface d’attaque externe de Contoso et rempli l’instance EASM avec des données exploitables.

### Tâche 3 : configurer le connecteur de données et l’espace de travail Log Analytics

Dans cette tâche, vous allez configurer une connexion de données de Defender EASM à un espace de travail Log Analytics qui sera utilisé pour Sentinel. Les informations sur les ressources ou insights Defender EASM peuvent être utilisées dans Log Analytics pour enrichir les flux de travail existants avec d’autres données de sécurité.

1. Vous devriez toujours vous trouver dans le Portail Azure **<https://portal.azure.com>**.
2. Dans la zone de recherche, recherchez **Espaces de travail Log Analytics**.
3. Sélectionnez l’espace de travail **law-sentinel** que vous avez utilisé dans l’exercice précédent.
4. Dans le volet de navigation de gauche, développez **Paramètres** et sélectionnez **Agents**.
5. Laissez la page telle quelle, ouvrez un autre onglet et connectez-vous au Portail Azure **<https://portal.azure.com>**.
6.  Dans la barre de recherche en haut, recherchez et ouvrez **Microsoft Defender EASM**.
7.  Sélectionnez votre espace de travail **EASM**.
8.  Dans le volet de navigation de gauche, développez **Gérer** et sélectionnez **Connexions de données**.
9.  Sous Log Analytics, sélectionnez **Ajouter une connexion**.
10. Nommez-la **law-sentinel**.
11. Basculez vers l’onglet précédent où l’espace de travail Log Analytics doit être ouvert.
12. Développez **Instructions de l’agent Log Analytics**.
13. Copiez l’**ID d’espace de travail** et la **clé primaire** dans le champ correspondant dans Defender EASM - Ajouter une connexion de données.
14. Dans Contenu, sélectionnez **Tout**.
15. Dans Fréquence, sélectionnez **Quotidien**.
16. Sélectionnez **Ajouter**.

Une fois la connexion créée, les tables de journal personnalisées sont créées dans l’espace de travail Log Analytics. Dans Sentinel, ces données peuvent ensuite être utilisées pour créer ou enrichir des incidents de sécurité, créer des plans d’investigation, entraîner des algorithmes d’apprentissage machine ou déclencher des actions de correction.

Vous avez correctement configuré la connexion entre Defender EASM et un espace de travail Log Analytics.

### Tâche 4 : consulter les tableaux de bord et les ressources d’étiquette

Dans cette tâche, vous allez consulter l’état de la sécurité de Defender EASM et obtenir des informations sur les résultats.

1. Vous devriez toujours vous trouver dans le Portail Azure **<https://portal.azure.com>**.
2. Dans la barre de recherche en haut, recherchez et ouvrez **Microsoft Defender EASM**.
3. Sélectionnez votre espace de travail **EASM**.
4. Dans le volet de navigation de gauche, développez **Tableaux de bord** et sélectionnez **Résumé de la surface d’attaque**

Les tableaux de bord Résumé de la surface d’attaque fournissent des informations clés et une vue d’ensemble des principales ressources affectées de votre surface d’attaque.

5. Consultez le tableau de bord **Résumé de la surface d’attaque**.
6. Dans le volet de navigation de gauche, sélectionnez **État de la sécurité**.
7. Passez en revue les différentes catégories pour identifier les vulnérabilités ouvertes.
8. Sous la catégorie **Ports ouverts**, sélectionnez **Serveurs web**.
9.  Sélectionnez l’adresse IP trouvée **34.223.124.45**.

Vous décidez d’étiqueter la ressource pour un examen plus approfondi.

10. Sélectionnez **Modifier la ressource**.
11. Sélectionnez **Créer une étiquette**.
12. Nommez-la **Ports ouverts**, puis sélectionnez **Ajouter**.
13. Affectez l’étiquette que vous venez de créer dans le champ **Étiquettes**.
14. Sélectionnez **Mettre à jour**.

Vous avez examiné l’état de la sécurité et étiqueté une ressource pour un examen plus approfondi.

### Tâche 5 : gérer les ressources

Dans cette tâche, vous allez gérer et classer les ressources découvertes.

1. Vous devriez toujours vous trouver dans le Portail Azure **<https://portal.azure.com>**.
2. Dans la barre de recherche en haut, recherchez et ouvrez **Microsoft Defender EASM**.
3. Sélectionnez votre espace de travail **EASM**.
4. Dans le volet de navigation de gauche, développez **Général**, puis sélectionnez **Inventaire**.
5. Sous Rechercher, dans le menu déroulant, sélectionnez **Étiquette**
6. Dans le menu déroulant ci-dessous, choisissez l’étiquette que nous avons créée à la tâche 4 **Ouvrir des ports**.
7. Sélectionnez **Recherche**.
8. Ouvrez la ressource trouvée **34.223.124.45**.
9. Sélectionnez la colonne **Composants Web**.

Vous identifiez que cette ressource est hébergée sur Amazon. Il existe également des CVE ouvertes sur certains composants, mais celles-ci ne sont pas actives, comme vous pouvez le voir dans les colonnes **Récent** et **Dernière connexion**. Celles-ci proviennent des exécutions de découverte antérieures.
Étant donné que cette ressource est hébergée par un tiers mais qu’elle fait toujours partie de votre surface d’attaque, vous la catégorisez en fonction de son rôle dans votre organisation.

10. Sélectionnez **Modifier la ressource**.
11. Sélectionner **Dépendance**.
12. Sélectionnez **Mettre à jour**.

>[!NOTE]Ici, vous choisissez Dépendance, car la ressource est une infrastructure appartenant à un tiers, mais fait partie de votre surface d’attaque, car elle soutient directement le fonctionnement de vos propres ressources.

13. Revenez à Inventaire en sélectionnant **X** en haut à droite et en créant une nouvelle recherche.
14. Modifiez la requête de recherche en **Nom de composant web - contient - Amazon**.
15. Sélectionnez **Recherche**.
16. Sélectionnez Toutes les ressources.
17. Sélectionnez **Modifier les ressources**.
18. Dans État, choisissez **Dépendance**, puis sélectionnez **Mettre à jour**.

Uniquement si l’état est défini sur **Inventaire approuvé**, les ressources sont représentées dans les graphiques de tableau de bord et sont analysées quotidiennement. Il est donc important d’examiner les ressources récemment découvertes et de modifier leur état en conséquence.

Dans le cadre de cet exercice, vous avez configuré Defender EASM, créé la découverte de l’environnement exposé à l’extérieur de Contoso. Vous avez des informations plus approfondies sur les ressources et leur configuration et vous avez géré des ressources afin que les tableaux de bord incluent uniquement les données dont Contoso est directement responsable.
