---
casestudy:
  title: "Étude de cas\_: concevoir des solutions avec les bonnes pratiques de MCRA et MCSB"
  module: 'Module 03: Design solutions that align with MCRA and MCSB'
---

Cet exercice d’étude de cas permet d’acquérir une expérience dans l’exécution de certaines tâches d’étude conceptuelle liées aux sujets appris dans ce module.

## Étude de cas : concevoir des solutions avec les bonnes pratiques de MCRA et MCSB
 
CONTOSO est une société de services de santé dont les bureaux principaux sont établis à Chicago et Londres, au Royaume-Uni.  
La société fournit des services de santé à ses clients dans ses installations situées à Chicago et dans la zone métropolitaine de Londres, au Royaume-Uni.  Les installations de Contoso comptent de nombreux hôpitaux disposant de médecins, d’infirmières et d’autres professionnels de la santé. Contoso a lancé la migration à l’échelle de l’entreprise de tous les services critiques vers le cloud. Cette migration inclut les serveurs locaux, les machines virtuelles et les appliances de gestion et de surveillance qui y sont associées.

Contoso a lancé sa migration vers le cloud, à l’exception de certaines données et applications qui doivent être hébergées localement en raison des exigences réglementaires et de conformité. Contoso définit un locataire Azure Active Directory (Azure AD). Cet Azure AD est synchronisé avec Active Directory Domain Services (AD DS), qui est géré sur des contrôleurs de domaine locaux. À mesure que la migration progresse, des abonnements Azure supplémentaires seront créés selon les besoins de chaque service, y compris les applications SaaS. Pour faciliter leur travail quotidien, la plupart des employés ont accès aux applications Microsoft 365.  
 
Pour assurer une connectivité continue, des tests VDI (Virtual Desktop Infrastructure) de base ont  
été lancés pour la plupart des catégories d’employés, telles que les responsables de comptes,  
l’équipe support, le personnel métier, le personnel des finances et le personnel des RH. La connectivité sécurisée est prise en charge via  
une passerelle de réseau privé virtuel (VPN) pour un ensemble limité d’utilisateurs et d’appareils. En outre,  
un pare-feu tiers a été déployé pour protéger le réseau local virtuel  
(VLAN) du serveur virtuel.  
 
Bien qu’ils se trouvent sur place avec leurs clients, les médecins utilisent des appareils mobiles  
qui stockent les données de suivi et de surveillance localement. Ces données sont protégées à l’aide d’un chiffrement du stockage propriétaire  
et chaque professionnel de la santé doit se connecter à son appareil à l’aide d’informations d’identification stockées localement avant d’accéder aux données. 
 
### Spécifications

À mesure que la migration cloud se poursuit et s’étend, Contoso prévoit de déplacer toutes les données  
et applications locales dans le cloud, à l’exception des applications non visées. 

* Déployer Microsoft 365 Defender et Defender pour le cloud pour améliorer les postures de sécurité de Contoso contre les personnes mal intentionnées 
* La stratégie de conformité Microsoft MCSB doit être appliquée à l’abonnement Azure. 
* Contoso souhaite identifier de manière proactive les éventuelles menaces et gérer activement la surface d’attaque. 
* Contoso souhaite gérer de manière centralisée les identités pour les prestataires externes et les patients ainsi que les employés internes. 
* Tous les appareils de point de terminaison doivent être gérés de manière centralisée et évalués en permanence pour s’assurer de leur conformité. 
* Les informations médicales protégées stockées sur les appareils mobiles utilisés par les professionnels de la santé seront déplacées vers le cloud suivant la stratégie de résidence des données pour se conformer aux réglementations régionales. 
* L’accès aux appareils mobiles sur le terrain doit être limité par la géolocalisation et nécessite un code biométrique comme authentification multifacteur.  
* Le partage de données entre les applications sur le même appareil doit être contrôlé.  
* Conformité aux exigences de la loi américaine HIPAA (Health Insurance Portability Accountability Act) et des services de santé nationaux (NHS) du Royaume-Uni. 
* Contoso souhaite gérer les administrateurs disposant de privilèges en suivant les principaux avec privilèges minimum et appliquer des stratégies d’accès juste-à-temps. 
* Contoso souhaite récupérer ses données en cas de sinistre et souhaite également conserver ces données de sauvegarde dans un emplacement sécurisé. En cas de sinistre dans leur région primaire, Contoso souhaite basculer vers la région secondaire. 
* Contoso souhaite s’assurer que l’entreprise suit l’approche Confiance Zéro pour valider tous les accès entrants.
* À mesure que les données et le traitement sont déplacés vers Azure, la passerelle VPN doit être configurée pour  
prendre en charge les connexions P2S sécurisées à partir d’appareils qui exécutent un éventail de systèmes d’exploitation  
de bureau et mobiles, y compris Windows, macOS, Android et autres.  

### Tâches de conception

* Quel plan Defender Contoso doit-il appliquer pour répondre à ses exigences de sécurité et d’entreprise ? 
* Que peut faire Contoso pour valider tous les accès entrants tout en suivant l’approche Confiance Zéro ? 
* Comment Contoso peut-il appliquer les stratégies NHS et HIPAA à son environnement cloud ? 
* Que doit utiliser Contoso pour bénéficier d’une visibilité de toutes les menaces et vulnérabilités existantes ? 
* Comment Contoso doit-il déployer et gérer la configuration de sécurité sur les appareils de point de terminaison ? 
* Comment Contoso peut-il bénéficier d’une visibilité des applications cloud utilisées et des données partagées en externe ? 
