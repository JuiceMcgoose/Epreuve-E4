# Stage
## BIG work in progress...
## Here I will be describing the different projects and thechnologies I worked on during my internship.

[:)](https://imgur.com/gallery/zPFhSqy)


## Gestion de partitions: LVM
...

## Docker et DockerFile
...

## Nextcloud/LAMP
...

## MariaDB
...

# Working with Ansible: 

## Intro

#### Ansible est un outil libre et open-source permettant de déployer et de maintenir ses applications et ses systèmes. Il utilise le protocole _SSH_ pour communiquer avec les hôtes distants. Les fichiers de configuration s'écrivent en langage *YAML*.

## L'inventaire
#### Les machines hosts sur lesquelles seronts deployees les playbooks sont stockes sous le fichier /ansible/hosts. Elles peuvent etres regroupees sous des groupes qui seront ensuite fait reference dans nos playbooks.
> /etc/ansible/hosts
![](file:///home/mehdi.allag/Pictures/Screenshot%20from%202023-01-17%2017-07-53.png![image](https://user-images.githubusercontent.com/78588391/212951194-754ee83f-83e6-4772-b88e-f1038b4817bb.png)


### Playbooks
#### Un playbook est un plan d'automatisation de taches. Les Playbooks Ansible sont exécutés sur un groupte ou ensemble de groupe d'hôtes, qui constituent ensemble un inventaire Ansible. Un playbook se divise en plusieurs parties.
Les playbooks sont constitues de modules qui executent automatiquement des taches sur notres group d'hotes.

Ci-dessous un example de Playbook constitue d'un seul "play" et de deux taches.
![image](https://user-images.githubusercontent.com/78588391/212954775-68950203-497d-437b-9d17-4587a7b812ba.png)

#### C'est apres la directve task que notre les actions pour notre tache vont pouvoir etre definis.
1. name: Description simple de la tache
2. ansible.builtin.package: Module Ansible qui va automatiquement utiliser le module specifique au gestionaire de paquet de l'hote(ansible.builtin.yum, ansible.builtin.aot etc). Pratique car nous evite donc de definir le gestionaire de paquets de chacunes des distributions.
3. name: nom du paquet a installer
4. state:  parametre qui definit si il faut installer (present) ou supprimer le paquet (absent)
5. Pour la seconde tache ---> script: indique que c'est un script qui vas s'executer.  
(le script en question) 

Ce play contient egalement un seconde tache qui execute un script bash sur l'hote. Nous utilisont le module script qui prand le nom du script et ses possbiles parametres.

![image](https://user-images.githubusercontent.com/78588391/212956562-8c69600d-78d2-41a7-9aaf-b818a09d6010.png)

## Un peu plus sur Ansible: Les roles

Les rôles fournissent un cadre et une structure bien définis pour définir nos tâches, variables,modèles et autres fichiers. Ainsi, nous pouvons les référencer et les appeler dans nos playbooks avec seulement quelques lignes de code, tandis que nous pouvons réutiliser les mêmes rôles sur de nombreux projets sans avoir à dupliquer notre code.

Demonstration du fonctionnement des roles en installent Nginx webserver et en remplacent la page par default de Nginx sous debian par une page modifie.
> Structure de notre role:
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2009-40-19.png)

1. Default va contenire des noms de variables.
2. Handlers: Sont des taches speciales qui se seront actives que via la directive "notify".
3. Tasks: Ensemble de nos taches qui se deploierons sur les machines hosts.
4. Templates: Permet de créer de nouveaux fichiers au format jinja2.

> Contenue du fichier tasks: 
  ![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2009-49-01.png)
  
  "Replace default page" va modifier la page html par default en prenant pour source index.html.j2, la page personnalise.
 
 > Les differentes variables qui peuvent etres appelles au seins de notre role:
 
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-07-08.png)

Pour appeller l'une de ces variables utiliser la syntax: "{{ **nom_de_variable** }}", qui seront souvent appeller dans tasks.

Notre page par default sera modifier de cette maniere: 

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-06-51.png)

**__(cliquer pour voir le deploiement du roles)__**
[![asciicast](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-58-16.png)](https://asciinema.org/a/SgPUVITOapHD1PwHm0kFlAqMP)
Les options -DC: 
1. Pour montrer la difference dans les fichiers de configuration et lors de l'execution des taches.
2. C Pour lancer le playbook en mode check. Cela ne va que simuller les changements, telechargements et mises en place des paquets par exemple etc. Option tres utile pour faire des tests et s'assurer que tout fonctionne bien. 

Il y a une "erreur" a la fin car le playbook essaye de simulier le redemarage d'un service, nginx... Ce n'est pas possible, soit le service redemarre, soit il ne redemmare pas :)

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

### Mise en place des regles de pare-feu

Dans notre scenario, notre client doit contacter le serveur pour accéder à certains services. Objectif : uniquement autoriser la connexion à ces services, et depuis ce client uniquement. Nous mettrons en place certaines règles de pare-feu ayant ces effets. 

Les regles a mettre en place: 

> 1. Apache via les ports 80/443
> 2. MariaDB via le port 3309
> 3. SSH via le port 22 
> 4. Bloquer toute autre connections 


![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-09%2016-59-13.png)

## Fail2ban

Fail2ban agit à une couche différente de la couche réseau de niveau 3 d'un pare-feu. Celui-ci bloque les paquets du protocole TCP. Mais le port 22 est encore ouvert et des connexions peuvent toujours avoir lieux. C'est là que rentre en jeu le logiciel Fail2ban en surveillant les entrées des logs de no services. Fail2ban offre de nombreuses options pour sécuriser notre serveur, pour limiter les attaques par brutes-force ou DDOS.

Les parametres a prendre en compte:
1. bantime 10m (Définie la durée du bannissement)
2. findtime 2m (Fourchette de temps pendant lequel les tentatives de connections amènent à un bannissement)
3. maxretry 3 (nombre de tentatives maximum)
4. ssh = yes ( S'applique sur ssh )


## Firewalld
...

# Script shell TCP: 
### Vérifie les ports TCP en écoute sur une machine distante et qui applique une serie de règles IPtables laissant les connexions ouvertes sur ces ports, depuis une liste de machine authorises.

1. Écrire des règles IPtables 
2. Écrire un script shell simple et efficace
3. Playbooks Ansible qui déploie le script sur un groupe de machines
4. Mettre en place un cron.

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-09%2017-19-03.png)

1. __machine_ip__ est un tableau contenant les machines autorisees.
2. __cible__: Machine sur laquelles les access seront restraints via IPtables.
3. __var__: Va contenire le resultat de notre script **awk**.


  **var=$(ss -tl4 | awk '/^LISTEN/ { split($4, a, ":"); print a[2];}')**  
  AWK est un language utilise pour la manipulation, modification et triage de fichier.
 
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-09%2017-43-01.png)



