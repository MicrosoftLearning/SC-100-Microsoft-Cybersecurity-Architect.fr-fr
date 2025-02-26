---
lab: 3
title: "Exercice\_5 - Repéage des menaces"
---


# Labo 3 - Exercice 5 - Recherche de contenu Microsoft Purview

Votre entreprise est confrontée à une menace sérieuse pour son intégrité et sa sécurité. Un nombre important d’e-mails malveillants ont été détectés. Votre tâche consiste à identifier les adresses d’expéditeur ou les lignes d’objet de ces e-mails. Une fois que vous avez identifié ces e-mails malveillants, vous devez les supprimer en masse.

## Partie 1 : concevoir une solution (obligatoire)

### Approche de conception

La première étape consiste à identifier les e-mails malveillants. Par conséquent, une analyse du flux de messagerie actuel est essentielle. Le portail Microsoft Defender fournit une vue d’ensemble de tous les flux de courriers sortant et entrant, ainsi que d’autres fonctionnalités d’examen de ce trafic. L’action de correction implique de supprimer les e-mails malveillants. 

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Identifier les e-mails malveillants|Microsoft Defender pour Office 365|Examiner le flux de courriers et analyser les en-têtes|
|Éliminer les risques provenant d’e-mails malveillants|Microsoft Defender pour Office 365|Supprimer les messages malveillants|

### Tâche 1 : examiner les messages malveillants

Vous allez examiner les e-mails entrants dans le portail Microsoft Defender et identifier ceux qui sont suspects et contiennent du contenu malveillant.

1. Connectez-vous au portail Microsoft Defender **https://security.microsoft.com** en tant qu’Allan Deyoung à l’aide de son compte d’**administrateur MOD**.
1. Dans le portail de Sécurité Microsoft, développez **E-mail et collaboration**, puis sélectionnez **Explorateur**.
1. Sur la page **Explorateur**, ajustez la période de la requête pour afficher tous les flux d’e-mails des 30 derniers jours, puis sélectionnez **Actualiser**.
1. Le résultat affiche tous les e-mails entrants et sortants. Examinez le flux d’e-mails et leurs objets.
1. Les e-mails avec l’objet « Vous avez des tâches à terminer aujourd’hui » apparaissent suspects.
1. Sélectionnez l’objet à examiner plus en détail.
1. Sur le nouveau volet **Vous avez des tâches à terminer aujourd’hui**, affichez les informations fournies et sélectionnez **Afficher l’en-tête**.
1. Dans le volet **En-têtes de message**, sélectionnez **Copier l’en-tête de message** et sélectionnez **Analyseur d’en-tête de message Microsoft**.
1. Un nouvel onglet s’ouvre dans le navigateur.
1. Sur la page **Analyseur d’en-tête de message**, collez l’en-tête du message et sélectionnez **Analyser les en-têtes**.
1. Passez en revue le résultat.

Vous avez examiné le flux de courriers dans le portail Microsoft Defender.

### Tâche 2 : effectuer une suppression massive d’e-mails malveillants

Vous avez conclu que les e-mails avec le sujet « Vous avez des tâches à terminer aujourd’hui » constituent des attaques par hameçonnage. Votre action de correction implique une suppression massive de ces e-mails à l’aide de PowerShell.

>[!NOTE] Vous devez avoir déjà installé le module PowerShell Exchange Online. Si ce n’est pas le cas, suivez les instructions d’installation du module.

1. Ouvrez une fenêtre PowerShell à privilèges élevés, en cliquant avec le bouton droit de la souris sur le bouton Windows et en sélectionnant **Windows PowerShell (administration)**.
1. Dans la fenêtre **Contrôle de compte d’utilisateur**, confirmez en cliquant sur **Oui**.
1. Saisissez la cmdlet suivante pour installer la dernière version du module PowerShell Exchange Online :

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirmez la boîte de dialogue de sécurité du référentiel non approuvé en appuyant sur **O** pour Oui, puis appuyez sur **Entrée**.  Ce processus peut prendre un certain temps.
1. Ouvrez une fenêtre PowerShell à privilèges élevés, en cliquant avec le bouton droit de la souris sur le bouton Windows et en sélectionnant **Windows PowerShell (administration)**.
1. Dans la fenêtre **Contrôle de compte d’utilisateur**, confirmez en cliquant sur **Oui**.
1. Entrez la cmdlet suivante pour vous connecter à Security &Compliance PowerShell :

    ```powershell
    Connect-IPPSSession
    ```

1. Lorsque la fenêtre **Se connecter** s’affiche, connectez-vous en tant que admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo) et utilisez le mot de passe d’administration de votre locataire.
1. Entrez la cmdlet suivante pour effectuer la recherche de contenu en spécifiant la période dans la cmdlet :

    ```powershell
    $Search=New-ComplianceSearch -Name "Purge phishing messages" -ExchangeLocation All -ContentMatchQuery '(Received:mm/dd/yyyy..mm/dd/yyyy) AND (Subject:"You have tasks due today")'
    Start-ComplianceSearch -Identity $Search.Identity
    ```
1. Entrez la cmdlet suivante pour supprimer définitivement les messages :

    ```powershell
    New-ComplianceSearchAction -SearchName "Purge phishing messages" -Purge -PurgeType HardDelete
    ---
You have successfully performed a mass-deletion of malicious mails.