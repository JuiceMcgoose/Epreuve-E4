# Stage
## BIG work in progress...
## Here I will be describing the different projects and thechnologies I worked on during my internship.

![:)](https://imgur.com/gallery/zPFhSqy)

## Hyperviseur Proxmox
Proxmox est un loggiciel libre de virualisation et de gestion de parc informatique. J'ai installer Proxmox sur un serveur sur lequel j'efectuerais mes differentes taches et projet tout au long de ce stage.

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2011-31-41.png)
## Gestion de partitions: LVM
...

## Docker et DockerFile
...

## Nextcloud/LAMP Stack
Nextcloud est un service de partage de fichiers libre et open-source qui nous donne contrôle sur nos fichiers, respect de nos documents privés et une forme avance de contrôle, car autogérés. Pour installer le service Nextcloud, il me sera nécessaire d'installer une pile de technologies complémentaires
__(LAMP/STACK Linux, Apache, mariaDB, PHP)__. Linux sera notre système d'exploitation, Apache notre serveur web, MariaDB le serveur de base de donnes, PHP le langage cote serveur gérant les pages dynamiques.  


## MariaDB
...

## RockyLinux/cockpit
...
Cockpit est un logiciel de gestion de serveur avec interface web. Pour les utilisateurs  aux capacités techniques limitées, il leur permet de ne pas avoir à utiliser l'interface de commandes, mais d'avoir néanmoins une interface plus lisible et légère que d'installer un environnement de bureau sur le serveur. 
Le paquet doit être localement installé sur le serveur/client avant de pouvoir accéder a l'interface web (machine-IP :9090).

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-10%2011-47-52.png)

# Working with Ansible: 

## Intro

#### Ansible est un outil libre et open-source permettant de déployer et de maintenir ses applications et ses systèmes. Il utilise le protocole _SSH_ pour communiquer avec les hôtes distants. Les fichiers de configuration s'écrivent en langage *YAML*.

## L'inventaire
#### Les machines hôtes sur lesquelles s'errons déployées les playbooks sont stockés sous le fichier /ansible/hosts. Elles peuvent être regroupées sous des groupes qui seront ensuite faits référence dans nos playbooks.

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

#### A suire...

# Lab reseau
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

### Mise en place des règles de pare-feu

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



