# Sommaire:

1. [Introduction](#introduction)
2. [Projets realises en cours de formation.](#projets-realises-en-cours-de-formation)
	1. [Routage sur vlan](#routage-sur-vlan)
	2. [Installation borne Wi-Fi](#borne-wifi)
	3. [GLPI](#glpi)
	4. [Serveur d'authentification](#srveur-d'authentification)
	5. [Annuaire LDAP](#annuaire-ldap)


# Introduction: 





# Projets realises en cours de formation

## Routage sur vlan
### Date de realisation: (30/06/2022) 
### ![Routage sur vlan](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/routage_allag_mehdi%2Bvpn-1.pdf) (30/06/2022)
### Competence mises en oeuvre: Mettre en place et verifier les niveaux d'habilitation associes a un service.

## Borne wifi
### (22/03/2022)
### ![Borne-wifi](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/ALLAG%20Mehdi%20wifi%20.pdf)
### Competences mises en oeuvre: 

## GLPI
### (12/05/2022)
### ![GLPI](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/GLPI-1.pdf)
### Competence mise en oeuvre: __Collecter, suivre et orienter des demandes/ Traiter les demandes concernant les services reseaux et systhems,applicatifs__ / Recensement et identification des ressources numérique. 

## Serveur d'authentification
### (05/01/2022)
### ![Serveur d'authentification](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/serveur_authentification.pdf)
### Competences mises en oeuvre: Exploitation des référentiels, normes et standards adoptés par le prestataire informatique. Mise en place et vérification des niveaux d’habilitation associés à un service. Gestion des sauvegardes.Vérification du respect des règles d’utilisation des ressources numériques

## Annuaire LDAP
### (22/02/2022)
### ![LDAP](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/Installation%20du%20service%20d%E2%80%99annuaire%20LDAP%20.pdf) 
### Competences mises en oeuvre:


## *Realisation faite en cours de formation:* ![Partage de fichiers](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/filebrowser_allag_mehdi-2.pdf) (07/11/2022)

#### Competences mises en oeuvre: Exploitation des référentiels, normes et standards adoptés par le prestataire informatique/Vérification du respect des règles d’utilisation des ressources numériques/

## *Realisation faite en cours de formation:* ![ActiveDirectory](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/activedirectory_mehdi-3.pdf) (24/11/2022)

#### Competences mises en oeuvre:


# Realisations en cours de Stage:

## Hyperviseur Proxmox
### Competences: Verifier les conditions de la continuite d'un service informatique. Gerer des sauvegardes.
Proxmox est un logiciel libre de visualisation et de gestion de parc informatique. J'ai installé Proxmox sur un serveur sur lequel j'effectuerais mes différentes tâches et projet tout au long de ce stage.

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2011-31-41.png)
## -Gestion de partitions: LVM
#### -Competence mise en oeuvre: Analyser les objectifs et les modalites d'organisation et mesurer leur visibilite/ Recenser et identifier les ressources numeriques.

La gestion des volumes logiques (LVM) est un système de gestion des disques utilisé pour gérer et organiser l'espace disque sur un système Linux. Il permet de créer des partitions virtuelles qui peuvent être redimensionnées et déplacées de manière dynamique, sans avoir à arrêter le système ou à démonter un système de fichiers.
Les trois parties centralles de LVM:

1. Volumes physiques (PV) : La première étape de l'utilisation de LVM consiste à créer un ou plusieurs volumes physiques (PV) sur le disque. Il s'agit de partitions de disque réelles qui seront utilisées pour stocker des données.
2. Groupe de volume (GV) : Sont des collections de volumes physiques depuis lesquelles nos volumes logiques seront creers.
3. Volumes logiques (LV) : Un volume logique est un périphérique de stockage virtuel qu'un système de fichiers peut utiliser.

Tache : Il etait question d'implémenter un RAID1 sous LVM sur un serveur avec disque linéaire configuré avec RAID. Il sera question de créer un nouveau volume physique que nous convertirons par la suite en volume RAID et de re-attacher ce volume au volume déjà existant.

## Docker et DockerFile
...

## Nextcloud/LAMP Stack: Deploiyer un service. Gerer des saubegardes. Recenser et indetifier les ressources numeriques.
Nextcloud est un service de partage de fichiers libre et open-source qui nous donne contrôle sur nos fichiers, respect de nos documents privés et une forme avance de contrôle, car autogérés. Pour installer le service Nextcloud, il me sera nécessaire d'installer une pile de technologies complémentaires
__(LAMP/STACK Linux, Apache, mariaDB, PHP)__. Linux sera notre système d'exploitation, Apache notre serveur web, MariaDB le serveur de base de donnes, PHP le langage cote serveur gérant les pages dynamiques.  


## RockyLinux/cockpit
...
Cockpit est un logiciel de gestion de serveur avec interface web. Pour les utilisateurs, il leur permet d'avoir acceer a un tableau de bord sur la machine, et de ne pas avoir à utiliser l'interface de commandes, mais d'avoir néanmoins une interface plus lisible et légère que d'installer un environnement de bureau sur le serveur. 
Le paquet doit être localement installé sur le serveur/client avant de pouvoir accéder a l'interface web (machine-IP :9090). J'installerais egallement un module de stockage complementaire, qui n'est pas la par defaut, via un role Ansible.

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2011-47-52.png)

# Working with Ansible: 

## Intro

### Competences:
#### Ansible est un outil libre et open-source permettant de déployer et de maintenir ses applications et ses systèmes. Il utilise le protocole _SSH_ pour communiquer avec les hôtes distants. Les fichiers de configuration s'écrivent en langage *YAML*.


## L'inventaire
#### Les machines hôtes sur lesquelles serrons déployées les playbooks sont stockés sous le fichier /ansible/hosts. Elles peuvent être regroupées sous des groupes qui seront ensuite faits référence dans nos playbooks.

![](file:///home/mehdi.allag/Pictures/Screenshot%20from%202023-01-17%2017-07-53.png)


### Playbooks
#### Un playbook est un plan d'automatisation de taches. Les Playbooks Ansible sont exécutés sur un groupe ou ensemble de groupe d'hôtes, qui constituent ensemble notre inventaire Ansible. Un playbook se divise en plusieurs parties.

Les playbooks sont constitués de modules qui exécutent automatiquement des tâches sur notre groupe d'hôtes.

Ci-dessous un example de Playbook constitue d'un seul "play" et de deux taches.
![image](https://user-images.githubusercontent.com/78588391/212954775-68950203-497d-437b-9d17-4587a7b812ba.png)

#### C'est apres la directive task que les actions pour notre tache vont etre definis.
1. name: Description simple de la tache
2. ansible.builtin.package: Module Ansible qui va automatiquement utiliser le module specifique au gestionaire de paquet de l'hote(ansible.builtin.yum, ansible.builtin.aot etc). Pratique car nous evite donc de definir le gestionaire de paquets de chacunes des distributions.
3. name: nom du paquet a installer
4. state:  parametre qui definit si il faut installer (present) ou supprimer le paquet (absent)
5. Pour la seconde tache ---> script: indique que c'est un script qui vas s'executer.  
(le script en question) 

Ce play contient également une seconde tache qui exécute un script bash sur l'hôte. Nous utilisons le module script qui prend le nom du script et même, des paramètres si besoin.

![image](https://user-images.githubusercontent.com/78588391/212956562-8c69600d-78d2-41a7-9aaf-b818a09d6010.png)

## Un peu plus sur Ansible: Les roles

Les rôles fournissent un cadre et une structure bien définis pour définir nos tâches, variables,modèles et autres fichiers. Ainsi, nous pouvons les référencer et les appeler dans nos playbooks avec seulement quelques lignes de code, tandis que nous pouvons réutiliser les mêmes rôles sur de nombreux projets sans avoir à dupliquer notre code.

Démonstration du fonctionnement des rôles en installent Nginx webserver et en remplacent la page par défaut de Nginx sous Debian par une page modifiée.
> Structure de notre role:
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2009-40-19.png)

1. Default va contenire nos variables.
2. Handlers: Sont des taches speciales qui se seront actives que via la directive "notify".
3. Tasks: Ensemble de nos taches qui se deploierons sur les machines hosts.
4. Templates: Permet de créer de nouveaux fichiers au format jinja2.

# Projets realises en cours de formation
> Contenue du fichier tasks: 
  ![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2009-49-01.png)
  
  "Replace default page" va modifier la page html par default en prenant pour source index.html.j2, la page personnalise.
 
 > Les differentes variables qui peuvent etres appelles au seins de notre role:
 
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-07-08.png)

Pour appeller l'une de ces variables, utiliser la syntax: "{{ **nom_de_variable** }}", qui seront souvent appeller dans tasks.

Notre page par default sera modifier de cette maniere: 

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-06-51.png)

**__(cliquer pour voir le deploiement du roles)__**
[![asciicast](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-58-16.png)](https://asciinema.org/a/SgPUVITOapHD1PwHm0kFlAqMP)
Les options -DC: 
1. **D** Pour montrer la difference dans les fichiers de configuration et lors de l'execution des taches.
2. **C** Pour lancer le playbook en mode check. Cela ne va que simuller les changements, telechargements et mises en place des paquets par exemple etc. Option tres utile pour faire des tests et s'assurer que tout fonctionne bien. 

Il y a une "erreur" à la fin, car le playbook essaye de simuler le redémarrage d'un service, nginx… Ce n'est pas possible, soit le service redémarré, soit-il ne redémarre pas :)

(**__cliquer pour voir le deploiement du roles)__**
[![asciicast](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2011-10-32.png)](https://asciinema.org/a/3sdVrff6tMoYslks06SHuqmO5)

### Role et variables Ansible

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2014-59-41.png)
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2015-00-01.png)
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2014-59-05.png)


#### A suire...

# Lab reseau

### Exploiter des referentiels, normes, et standards adoptees par le prestataire informatique. Evaluer les indicateurs de suivie d'un projet et analyser les ecarts.

Nous trouverons un client installé sous ![RockyLinux](https://rockylinux.org/), et un serveur hébergent différents services web sous Debian. Les deux se trouvant sur des réseaux différents. En intermédiaire, un pare-feu logiciel pfSense permettra le routage et le filtrage des connexions entre les deux réseaux.
Ci-dessous un schéma du lab en question à mettre en place :
![lien du lab](https://github.com/JuiceMcgoose/assets/blob/main/lab_reseau_mehdi.drawio.png) 

### Mise en place des différentes machines sous le nœud Proxmox:
Il sera tout d'abord question de configurer nos différentes machines pour qu'elles puissent communiquer entre elles.
> Notre noeud proxmox se trouve sous le reseau **172.30.112.0/24** sa gw en **172.30.112.0.254**
Le client reçoit automatiquement une IP(172.30.112.191) dans ce réseau via DHCP.

Le pfSense devra avoir deux interfaces, une dans chaque réseau. L'IP par défaut de l'interface pfSense qui nous permet d'accéder à l'interface web est 192.168.1.1, or, notre serveur dans le réseau 10.8.0.0/24, il faudra également changer cela.

Configuration finales des interfaces pfsense.
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2011-43-40.png)

Il faudra mettre en place une nouvelle route sur chacune des machines pour permettre la communication vers les différentes interfaces de notre pare-feu.
Pour notre réseau LAN, celui-ci ne dispose que d'une seule route possible. Pour notre réseau WAN en revanche, deux chemins de transports sont disponibles, l'un en direction du LAN, l'autre en direction du Proxmox et du réseau externe. 

> Routage serveur
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2014-15-19.png)

> Routage client
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2014-14-22.png)

> Passage des paquets
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2017-43-57.png)

### Mise en place des règles de pare-feux

Dans notre scenario, notre client doit contacter le serveur pour accéder à certains services. Objectif : uniquement autoriser la connexion à ces services, et depuis ce client uniquement. Nous mettrons en place certaines règles de pare-feu ayant ces effets. 

Les règles à mettre en place : 

> 1. Apache via 80/443
> 2. MariaDB via le port 3306
> 3. SSH via le port 22 
> 4. Bloquer toute autre connections 


![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-09%2016-59-13.png)

## Fail2ban

Fail2ban agit à une couche différente de la couche réseau de niveau 3 d'un pare-feu. Celui-ci bloque les paquets du protocole TCP. Mais le port 22 est encore ouvert et des connexions peuvent toujours avoir lieux. C'est là que rentre en jeu le logiciel Fail2ban en surveillant les entrées des logs de no services. Fail2ban offre de nombreuses options pour sécuriser notre serveur, pour limiter les attaques par brutes-force ou DDOS.

Les options a prendre en compte quand nous configurerons Fail2ban pour le service ssh:
1. bantime 10m (Définie la durée du bannissement)
2. findtime 2m (Fourchette de temps pendant lequel les tentatives de connections amènent à un bannissement)
3. maxretry 3 (nombre de tentatives maximum)
4. ssh = yes ( S'applique sur ssh )


## Firewalld
...

# Script shell TCP: 
### Vérifie les ports TCP en écoute sur une machine distante et qui applique une série de règles IPtables laissant les connexions ouvertes sur ces ports, depuis une liste de machine autorisés.
### Competences: Réaliser les tests d’intégration et d’acceptation d’un service. Planifier les activités. Déployer un service. 

#### Il nous faudrat:

1. Écrire des règles IPtables 
2. Écrire un script shell simple et efficace
3. Faire Playbooks Ansible qui déploie le script sur le groupe de machines
4. Ecrire et mettre en place un cron.

IPTables est un logiciel libre de pare-feux inclut dans le Kernel, permettant de mettre en place des regles de traffic entrant et sortant.


![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-09%2017-19-03.png)

1. __machine_ip__ est un tableau contenant les machines autorisees.
2. __cible__: Machine sur laquelles les access seront restraints via IPtables.
3. __var__: Va contenire le resultat de notre script **awk**.


  **var=$(ss -tl4 | awk '/^LISTEN/ { split($4, a, ":"); print a[2];}')**  
  (AWK est un language utilise pour la manipulation, modification et triage de fichier.)
  
La commande iptables -L -v -n permet de voir quelles règles sont définies pour la table filter qui est la table par défaut lorsque non spécifiée. 
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-09%2017-43-01.png)


## Mettre en place son environement d'apprantisage personnel:
### ArchLInux + gestionaire de fenetres DWM/DMENU

### J'autoheberge plusieurs services axes vers une philosophie de logiciel libre et open-source, en ayant pour objectif d'avoir plus de controle sur mes donnes + environement de bureau personnalise avec gestionnaire de fenetre et pile de logiciels libre et open-sources.(Zathura, neomutt, Pacman, ST, etc).
### Mise en place d'un server mail (90% fonctionnelle )
![mx record](https://github.com/JuiceMcgoose/assets/blob/main/mx_record.png)
### Les enregistrements MX sont utilisés pour acheminer les mails électronique associé à un nom de domaine, vers le serveur de messagerie approprié, par exemple, mail.powerful.software dans mons cas.

### Mise en place d'un service autoheberger sous licence libre a utilisation personnel. Ici, un logiciel de gestion et de sauvegardes de photos/videos simillaire a GooglePhoto deployes via une image DockerCompose.
### ![immich](https://github.com/JuiceMcgoose/assets/blob/main/pic-window-230303-1401-04.png)

### VIM

#### Vim est un éditeur de texte libre et gratuit, basé sur une l'interface de commandes et hautement personnalisable pour Unix.



## Gerer son indentite professionnelle: 
### https://github.com/JuiceMcgoose/ 

![CV](https://github.com/JuiceMcgoose/Epreuve-E4/blob/main/CV.pdf)

## Outils et stratégies de veille informationnelle.

### Ci-dessous les principales sources d'information que j'utilise pour ma veille informationnelle:

### https://www.reddit.com/r/ITCareerQuestions/
#### Communauté conçu pour aider toute personne travaillant dans le domaine de l'informatique ou intéressée par celui-ci à poser des questions relatives à sa carrière, ou future carrière. M'a beaucoup aidé pour me rendre compte des differents choix de carrieres venants de professionnels.

### https://www.reddit.com/r/networking/
#### Discussion sur les réseaux d'entreprise. protocles et reseaux informatique -- Routeurs, commutateurs, le sans fil, les pare-feu etx. Beaucoup d'informations sur Cisco, Juniper...

### https://news.ycombinator.com/ 

### https://www.reddit.com/r/cybersecurity/
#### Une communauté pour les professionnels techniques actuels ou en devenir afin de discuter de la cybersécurité, des menaces, etc.

[:)](https://imgur.com/gallery/zPFhSqy)



