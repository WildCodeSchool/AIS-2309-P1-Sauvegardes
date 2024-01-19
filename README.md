# AIS-2309-P1-Sauvegardes

# Membres du groupes
Le sujet des sauvegardes sera abordé par : 
Lucas DEGRET, Julien LE BRIS et Valentin COCHIN

## Présentation du projet : Besoins initiaux
Une entreprise d’environ 200 à 300 personnes a besoin d’une nouvelle infrastructure. Pour cela, trois sujets principaux s’offrent à nous :
	Sujet 1 : la refonte du réseau soit un nouveau LAN.
	Sujet 2 : un site distant avec déploiement de succursales.
	Sujet 3 : des sauvegardes.
 
Concernant les sauvegardes, il faut mettre en place un système de sauvegarde unifié qui contient les éléments suivants :
	- Serveurs sous Windows et Linux.	
	- Serveurs physiques et VM.
	- Cluster d’hyperviseurs proxmox.



# Sujet 3 :
## Introduction
Actuellement, il n’existe pas de plan de sauvegarde dans l’entreprise ce qui peut être très compromettant. Cela peut amener à une perte du site internet,  des données clients et des commandes perdues, etc.
Pourquoi mettre en place un système de sauvegarde ? 
C’est une stratégie d’entreprise qui permet de prévenir toute perte de données, d’avoir un plan de secours en cas de défaillance matérielle, des sauvegardes régulières en cas de contrôle des autorités fiscales, une protection contre les cyberattaques, un meilleur suivi de la relation client, un archivage des données facilité, un gain de compétitivité vis-à-vis des concurrents, une productivité améliorée, une meilleure gestion du temps et une tranquillité d'esprit face aux imprévus.
Toutes ces raisons nous ont amenés à mettre en place ce projet. La gestion de ce dernier sera basée sur la méthode scrum avec un Scrum Master et un Product Owner. Les rôles seront attribués à une personne différente chaque semaine.
Le Product BackLog a été réalisé sur Trello et servira pour toute la durée du projet. Il contient les éléments nécessaires à l'amélioration du projet. Un sprint backlog suit la liste des éléments du product backlog et définit les objectifs de cette semaine.

# Difficultés : 
## Le contexte
La première difficulté rencontrée est d'analyser une infrastructure qu’on ne connaît pas. Il était important de déterminer le nombre de services installés, le nombre d’employés et les outils utilisés pour avoir une approximation de la taille des données qu’on allait récupérer afin de s’assurer une bonne capacité de sauvegarde. 
Suite à la découverte du projet, l’important est de bien faire la distinction entre la partie physique et virtuelle et la gestion de ces derniers.  
Dans toute entreprise, quelle qu'elle soit, il est important d’ajouter de la redondance pour éviter la perte définitive des données. Nous avons dû réfléchir ensemble à une solution adaptée pour la conception de cette grande infrastructure.
Aussi, il était difficile pour nous d’apporter du concret, car l’environnement n’est pas pleinement réalisable en test compte tenu de la taille des données et du nombre de serveurs à reproduire.

# Solutions : 
## Introduction contexte : 
Une première discussion a été effectuée avec le client afin d’avoir une idée générale du sujet. 
Nous avons communiqué avec le groupe 1 pour avoir une idée globale de la refonte de l’infrastructure et connaître l’existant. Nous avons pu déterminer que l’infrastructure était composée de 230 utilisateurs divisés en plusieurs services : Le services généraux, la logistique, le marketing, les achats, le SI, la finance, la RH et la direction.
De plus, l’entreprise comporte plusieurs outils, nous avons donc différencié ces derniers. Il y a des données Windows pour l’active directory (AD), des données Linux pour le site Intranet et l’hébergement du site, des données pour les mails utilisateurs, des données clients qui comportent la base de données des clients et leurs commandes et les fichiers utilisateurs sur un NAS. Il est intéressant de différencier les sauvegardes fichiers selon les services.

# Solution contexte : Quoi ? Quand ? Où ?
La solution serait d'apporter un environnement de sauvegarde physique et un environnement Cloud avec une solution de sauvegarde. Différentes solutions de sauvegarde sont possibles et s’offrent à nous comme Veeam, Acronis Backup, Rsync etc. Nous avons décidé d'utiliser Acronis. 
Nous nous sommes basés sur la politique de sauvegarde 3-2-1. La règle est d’avoir au minimum trois copies des données sur deux supports différents, avec une copie stockée en dehors du site. 
Quoi ? Nous en avons conclu que la marge des données sauvegardées allait être conséquente et importante. Avec le responsable de l’entreprise, il a été établi qu’il y a environ 15 To de données à sauvegarder.
Quand ? La sauvegarde sera effectuée quotidiennement de façon incrémentale, avec une sauvegarde hebdomadaire complète, dotée d’une politique de rétention de 9 mois.
Où ? Un NAS rackable sera situé dans la salle serveur de l’infrastructure. Un autre NAS sera situé dans un étage du bâtiment. La sauvegarde dans le Cloud sera située en France.     
L’infrastructure sera équipée d’un onduleur. Celui-ci est situé sur un réseau électrique différent et sécurisé. Donc il ne sera pas pris en compte dans le sujet actuel.
Concernant les utilisateurs, seulement les Administrateurs système et le DSI pourront avoir un accès au panel de contrôle général de la sauvegarde et avoir un accès au document de la solution de sauvegarde. De plus, le reste des utilisateurs doit pouvoir créer un ticket auprès de l’équipe IT habilitée afin de récupérer des données perdues.

# Choix techniques 
Équipements physiques : un NAS rackable, un NAS bureautique agrémentés de disques durs HDD SATA.
Un NAS doit être redondant. Donc chaque NAS aura un RAID sur les disques durs. Nous avons décidé d’installer un RAID 10 car il permet de combiner les performances et d’apporter une redondance supplémentaire. Il est plus réactif et permet des reconstructions plus rapides.
Sur une sauvegarde complète de 15 To de données à sauvegarder. Nous avons une rétention de 9 mois, soit 270 jours et 10 Go de sauvegarde incrémentielle qui viennent s’ajouter. En comptant le RAID et les évolutions futures, chaque NAS sera équipé de 50 To de stockage. 
L’infrastructure sera composée d’un NAS synology DS423+ (550), d’un NAS RS422+ (700e) et 8 disques durs de 12 To. Donc un total de 4090 euros pour la partie physique. 

La solution Cloud : 
Pour la solution Cloud, nous avons donc choisi la solution d’Acronis. Concernant le coût de la sauvegarde dans le Cloud, celle-ci est évaluée par rapport à l’espace de stockage utilisé et est généralement évaluée en termes de coût au teraoctet. Ici, Acronis Cloud Storage propose une solution à 189€ l’année (419€ pour 3 ans, 589€ pour 5 ans) pour un espace de stockage de 250go, sur lequel nous mettrons les sauvegardes incrémentielles. 
Les logiciels utilisés :
Le prestataire choisi est “Acronis” avec son offre “Acronis Cyber Protect  Advanced“ à 1 009,00 € la licence. Elle permet de sauvegarder et d’assurer la protection d'un seul hôte virtuel VMware, vSphere ou Microsoft Hyper-V et un nombre illimité de machines virtuelles de son environnement. Nous avons actuellement 4 clusters à sauvegarder donc nous prendrons 4 licences. Ces licences seront gérées via un serveur de gestion pour unifier la sauvegarde.
Test réalisés
Comme annoncé précédemment, nous avons décidé d’utiliser Acronis pour les sauvegardes. Cependant, les tests ont été réalisés sur le logiciel Veeam backup parce que l’environnement de test était plus favorable. Nous avons installé Proxmox sur une machine virtuelle pour avoir un aperçu du logiciel et de ses fonctionnalités. De plus, nous avons installé Veeam backup sur un windows serveur 2022 situé sur une machine virtuelle. En amont, un schéma a été réalisé pour avoir un aperçu global de l’infrastructure de la solution de sauvegarde proposée pour le moment. Le schéma évolue en fonction des propositions.

# Améliorations
Apporter une sauvegarde hors ligne (offline). Par exemple, une copie sur un disque dur externe en isolant le matériel dans un endroit sûr. C’est une assurance, car la sauvegarde n’est pas connectée au réseau et ne sera pas aussi vulnérable aux dommages causés par les logiciels malveillants.
Réaliser des documents techniques du projet une fois que les tests seront concluants. Cette documentation pourra comporter plusieurs procédures : la démarche à suivre si un matériel tombe en panne, comment les sauvegardes sont effectuées, comment restaurer les données pour un utilisateur, etc.
Ajouter du matériel supplémentaire en cas d’évolutions de l’infrastructure. Dans cette période d’investissement, il est intéressant de rajouter des NAS et des disques durs en plus dans la solution de base afin d’augmenter la capacité de stockage si l’entreprise est en expansion. Cela revient à alimenter la réserve du service informatique et de pouvoir intervenir dans l’immédiat si besoin. 
