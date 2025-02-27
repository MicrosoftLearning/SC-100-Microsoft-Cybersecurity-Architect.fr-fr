---
lab: 3
title: "Exercice\_2 - Déléguer des demandes des personnes concernées"
---


# Labo 3 - Exercice 2 - Déléguer des demandes des personnes concernées

Contoso Ltd. prépare la certification ISO-27001. Dans le cadre de cette préparation, ils doivent implémenter un processus pour les demandes des personnes concernées relatives au RGPD. L’entreprise utilisera la fonctionnalité Demandes des personnes concernées Microsoft Priva et intégrera le nouveau flux de travail dans son processus d’audit de conformité interne. 

En tant qu’expert architecte en cybersécurité, vous allez déléguer la gestion des DPC européennes et configurer des autorisations de lecture pour l’audit. Pour vous assurer que les employés qui gèrent les cas de DPC ne gèrent pas aussi la fonctionnalité Gestion des risques de confidentialité, vous allez créer un groupe personnalisé de rôles en lecture seule. Les groupes de rôles intégrés accordent trop d’autorisations pour l’audit. 

Vous attribuez aux employés choisis les rôles nécessaires pour gérer les demandes des personnes concernés ou l’audit, en suivant le principe du moindre privilège. Pour terminer la stratégie de conformité, vous allez utiliser la version d’essai de Microsoft Priva et vérifier que les journaux d’audit sont activés dans votre locataire. Étant donné que l’audit de conformité a lieu tous les deux mois, vous augmentez la durée de rétention des demandes des personnes concernées afin d’éviter les périodes non couvertes entre les audits. 

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour répondre aux exigences de Contoso Ltd. liées à son expansion en Europe.

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Permettre à votre environnement de gérer les demandes des personnes concernées
- Une équipe désignée doit gérer les DPC.
- Les limites de rétention des DPC doivent être modifiées pour s’adapter à la planification de l’audit.

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Microsoft Priva propose des solutions pour gérer les demandes des personnes concernées. Examinez les contrôles et les stratégies actuels. Utilisez le portail de conformité Microsoft Purview pour passer en revue les configurations actuelles et déterminer les ajustements qui doivent être implémentés pour répondre aux exigences de la région vers laquelle ils s’étendent.

La troisième phase consiste à élaborer le concept de la solution. L’examen permet de conclure qu’il est évident que permettre à des employés spécifiques de gérer les DPC est la meilleure façon de répondre à toutes les exigences.  

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Permettre à votre environnement de gérer les demandes des personnes concernées|Centre d’administration et Microsoft Purview|Affecter des licences Privé et vérifier que le journal d’audit unifié est activé|
|Une équipe désignée doit gérer les DPC.|Rôles Microsoft Purview|Créer un groupe de rôles avec des autorisations pour gérer les DPC et affecter les employés désignés|
|Les limites de rétention des DPC doivent être modifiées pour s’adapter à la planification de l’audit.|Gestion des risques de confidentialité Microsoft Purview|Utiliser une action d’amélioration pour définir une limite de rétention de 90 jours pour les DPC|

## Partie 2 : implémenter la solution (facultatif)

## Tâche 1 : activer la licence d’essai Microsoft Priva

Dans les deux premières tâches, vous allez vérifier les conditions préalables nécessaires à l’utilisation des fonctionnalités de Microsoft Priva. Vous devez activer la licence d’essai Microsoft Priva et vous assurer que les journaux d’audit sont activés dans votre locataire.

1. Connectez-vous à la **machine virtuelle** avec les informations d’identification de l’administrateur.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **https://compliance.microsoft.com** et connectez-vous au portail de conformité Microsoft Purview en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit vous être fourni par votre fournisseur d’hébergement de labo.
3. Lorsqu’il vous est demandé de rester connecté, sélectionnez **Non**.
4. Dans le volet de gauche, sélectionnez **Gestion des risques de confidentialité - Vue d’ensemble** ou **Demandes des personnes concernées**.
5. Si la version d’essai n’est pas active, sélectionnez **Activer la version d’essai** en haut de la page.

Si la version d’essai est déjà active dans votre labo, vous devez toujours vérifier la quantité exacte de demandes des personnes concernées contenues dans votre licence dans le Centre d’administration.

6. **Connectez-vous** au **Centre d’administration Microsoft 365****https://admin.microsoft.com/**.
7. Dans le volet de gauche, sélectionnez **Facturation** et **Vos produits**.
8. Recherchez la licence **Gestion des risques de confidentialité Priva**.
9. Recherchez la licence **Gestion de la confidentialité - Demandes des personnes concernées** et le nombre de cas inclus.

Vous avez vérifié que votre locataire M365 dispose de licences Microsoft Priva actives.

## Tâche 2 : vérifier si les journaux d’audit sont activés

Pour que les fonctionnalités de Gestion des risques de confidentialité fonctionnent, l’enregistrement d’audit doit être actif dans votre locataire.

1. Ouvrez une fenêtre **PowerShell** à privilèges élevés en sélectionnant le menu Démarrer avec le bouton droit de la souris, puis sélectionnez **Windows PowerShell** et **exécutez en tant qu’administrateur**.
2. Saisissez la cmdlet suivante pour installer la dernière version du module PowerShell Exchange Online :
    ```powershell
    Install-Module -Name ExchangeOnlineManagement
    ```
3. Confirmez la boîte de dialogue de sécurité Nuget et la boîte de dialogue de sécurité du référentiel non approuvé en appuyant sur Y pour Oui, puis appuyez sur Entrée. Ce processus peut prendre un certain temps.
4. Entrez la cmdlet suivante pour vous connecter au service Exchange Online :
    ```powershell
    Connect-ExchangeOnline
    ```
5. Dans le formulaire **Connectez-vous à votre compte**, connectez-vous avec les informations d’identification de l’administrateur.
6. Après la connexion à Exchange Online PowerShell, entrez :
    ```powershell
    Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
    ```
7. Une valeur **True** pour _UnifiedAuditLogIngestionEnabled_ est renvoyée.
8. Si une valeur **False** est renvoyée, activez le journal d’audit avec la commande :
    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```
9. Un avertissement indiquant que l’application de la modification peut prendre jusqu’à 60 minutes est renvoyé. Le journal d’audit est désormais activé dans votre locataire. Vous pouvez vérifier ultérieurement avec la commande mentionnée précédemment.

Vous avez confirmé que les journaux d’audit sont activés dans votre locataire.

## Tâche 3 : créer un groupe de rôles personnalisé et lui attribuer les employés désignés

Dans cette tâche, vous allez créer le groupe personnalisé de rôles en lecture seule pour l’audit de conformité Contoso Ltd. et y affecter les employés désignés.

1. Connectez-vous au **portail de conformité Microsoft Purview****https://compliance.microsoft.com/**.
2. Sélectionnez l’onglet **Autorisations** sous l’onglet **Rôles et portées** dans le volet gauche.
3. Sélectionnez **Rôles** sous l’élément Solutions Microsoft Purview.
4. Créez un groupe de rôles avec les paramètres suivants :
    |Paramètre|Valeur|
    |----|----|
    |Nom|Audit de conformité interne en lecture seule|
    |Description|Ce groupe de rôles contient tous les rôles nécessaires pour l’audit bi-mensuel de l’état de la conformité de Contoso Ltd.|
    |Rôles|Journaux d’audit en lecture seule, cas en lecture seule, visionneuse de gestion Priva|
    |Utilisateurs|Grady Archie|
5. Sélectionnez **Suivant** sur **Ajouter des rôles au groupe de rôles** et passez à la tâche suivante sans fermer la boîte de dialogue.

Vous avez créé un groupe de rôles personnalisé avec les autorisations minimales nécessaires et affecté les employés désignés.

## Tâche 4 : affecter des employés et vous-même aux groupes de rôles intégrés

Vous devez maintenant attribuer les autorisations restantes pour la gestion des demandes des personnes concernées à l’aide des groupes de rôles intégrés.

*(Passez au point 4. si vous êtes toujours dans le menu Rôles et portées)*
1. **Connectez-vous** au **portail de conformité Microsoft Purview****https://compliance.microsoft.com/**.
2. Dans le volet de gauche, sélectionnez **Rôles et portées** > **Autorisations**.
3. Sélectionnez **Rôles** sous l’élément **Solutions Microsoft Purview**.
4. Ajoutez **Irvin Sayers** au groupe de rôles **Administrateurs des demandes des personnes concernées**.
5. Ajoutez **Alex Wilber** et **Joni Sherman** au groupe de rôles **Approbateurs des demandes des personnes concernées**.
6. Ajoutez le compte Administrateur **administrateur MOD** et **Megan Bowen** aux groupes de rôles **Administrateurs de gestion de la confidentialité** et **Administrateurs des demandes des personnes concernées**.

Vous avez maintenant attribué toutes les autorisations nécessaires à tous les employés pour gérer les demandes des personnes concernées.

## Tâche 5 : configurer la limite maximale de conservation des données pour les demandes des personnes concernées

Pour l’audit de conformité bi-mensuel, vous devez configurer la limite de conservation pour les demandes des personnes concernées dans cette tâche.

[!NOTE] L’application des modifications de vos groupes de rôles peut prendre jusqu’à 30 minutes, ce qui est nécessaire pour afficher la fonctionnalité des demandes des personnes concernées. Si vous venez de vous accorder les autorisations à la tâche 4, vous devrez peut-être attendre que les modifications prennent effet.

1. **Connectez-vous** au **portail de conformité Microsoft Purview****https://compliance.microsoft.com/**.
2. Dans le volet de gauche, sélectionnez **Gestionnaire de conformité**, puis sélectionnez l’onglet **Actions d’amélioration**.
3. En haut de la page, sélectionnez le filtre **Solutions :**, puis vérifiez **Gestion des risques de confidentialité Priva** et **Demandes de droits des personnes concernées Priva**.
4. Sélectionnez **Activer et appliquer les limites de conservation des données pour les données impliquées dans les demandes des personnes concernées**.
5. Cliquez sur **Affecter à l’utilisateur** > recherchez **Administrateur MOD** > **Affecter**, ce qui affecte l’administrateur MOD en tant que propriétaire de l’action d’amélioration.
6. Lisez les détails de l’amélioration.
7. Sélectionnez **Lancer maintenant** en bas de la description pour entrer directement les paramètres de demande des personnes concernées.
8.  Sélectionnez l’onglet **Période de conservation des données**.
9.  Définissez la valeur **Données collectées et rapports** sur 90 jours, puis sélectionnez **Enregistrer**.
10. Fermez l’onglet dans Edge.
11. Sélectionnez **Modifier les détails** en haut de la page de l’action d’amélioration.
12. Définissez le **statut de l’implémentation** sur **Implémenté**.
13. Sélectionnez **Enregistrer et fermer** en bas de la page.

Vous avez augmenté la limite de conservation des données des demandes des personnes concernées et mis à jour l’action d’amélioration.

Vous avez terminé la configuration de la fonctionnalité des demandes des personnes concernées et des cas de gestion délégués en conséquence. Vous pouvez passer à l’exercice suivant.
