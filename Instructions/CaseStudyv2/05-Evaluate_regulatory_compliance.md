---
casestudy:
  title: "Étude de cas\_: évaluer une stratégie de conformité réglementaire"
  module: 'Module 05: Design solutions for regulatory compliance'
---

Cet exercice d’étude de cas permet d’acquérir une expérience dans l’exécution de certaines tâches d’étude conceptuelle liées aux sujets appris dans ce module.

## Étude de cas : évaluer une stratégie de conformité réglementaire

Contoso Pharma est une société pharmaceutique internationale présente en Amérique du Nord et en Europe. Contoso Pharma dispose de charges de travail locales et dans Azure. L’objectif est que l’ensemble des charges de travail soient entièrement dans Azure et qu’il existe des charges de travail minimales en local dans les deux prochaines années. Voici une liste des principales charges de travail :

- Machines virtuelles (Windows et Linux)
- Comptes de stockage
- Key Vault
- PaaS SQL et SQL sur des machines virtuelles

Contoso Pharma dispose également d’un réseau VPN site à site entre le siège social de Redmond et le bureau principal de Londres. Ce réseau VPN permet aux ressources locales de communiquer.

Contoso Pharma dispose d’un environnement hérité à Redmond composé de quelques Windows Server 2012 exécutant un serveur web utilisé par l’application qui interroge la base de données pour rechercher les informations du client. Lors d’une enquête, il a été noté que la communication du serveur web hérité avec la base de données s’effectue via HTTP.

### Exigences de conception

Contoso Pharma a des besoins de conformité différents en fonction des charges de travail, comme indiqué dans le tableau ci-dessous :

| **Charge de travail** | **Type de données** | **Norme de conformité** |
|:---:|:---:|:---:|
| Machines virtuelles Windows | Informations sur les titulaires de cartes de crédit | PCI DSS |
| PaaS SQL | Informations sur la santé des patients | HIPAA |
| Comptes de stockage | Informations sur les titulaires de cartes de crédit | Comptes PCI DSS |

Pour être conforme à ces normes, Contoso Pharma doit pouvoir :

- Superviser la progression de la conformité au fil du temps
- Interdire aux propriétaires de charges de travail de provisionner des ressources qui ne sont pas conformes à ces normes
- S’assurer que les nouveaux abonnements déployés dans l’environnement utilisent les normes requises par défaut
- S’assurer que les ressources provisionnées sur chaque emplacement géographique conservent les données dans la région source à des fins de souveraineté des données

### Tâches de conception

* Quel outil permet de s’assurer que Contoso Pharma est en mesure d’analyser son état de conformité au fil du temps ? Sélectionnez l’option la plus appropriée.
* Quel est le service dans Azure qui doit être utilisé pour que les propriétaires de charge de travail puissent créer uniquement des ressources qui respectent les normes requises ?
* Quelle option doit être utilisée pour s’assurer que les propriétaires de charges de travail conservent les données à l’emplacement géographique approprié quand ils créent des ressources ?
* Comment la société Contoso Pharma peut-elle vérifier que les machines virtuelles qui ont été provisionnées sont conformes à la norme PCI DSS et connaître la procédure à suivre pour corriger le problème si ce n’est pas le cas ?
* Le chiffrement des données est indispensable pour répondre aux exigences de confidentialité. Quelles sont les phases de données auquel vous devez appliquer le chiffrement ?
* Quel service Azure pouvez-vous utiliser pour appliquer le chiffrement des données aux différentes charges de travail ?
