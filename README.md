# Stage
## BIG work in progress...
## Here I will be describing the different projects et thechnologies I worked on during my internship.

### Here is a link to a screenshot:
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
#### Pour commencer il nous faudrat une liste de machine distantes sur lesquelles deployer no Playbooks L'inventaire des machines se fais sous: 
> /etc/ansible/hosts
[](file:///home/mehdi.allag/Pictures/Screenshot%20from%202023-01-17%2017-07-53.png![image](https://user-images.githubusercontent.com/78588391/212951194-754ee83f-83e6-4772-b88e-f1038b4817bb.png)
#### Nous pouvons regrouper les machines sous differents groupes, ici, il n'y en a qu'un. Notre Playbook pourra specifiquement pointer vers l'un de ces groupes, ou sur tout l'inventaire.  

### Playbooks
#### Il lance une certaine série d'activités à êtres exécutées sur les machines. Un playbook se divise en plusieurs parties :
1. Le Play : Qui définissent une certaine sériée d'activités à êtres exécutées sur les machines. 
2. Les taches : Sont les actions qui seront effectuer sur les serveurs. Cela peut être un script, une commande, une action sur un service tournant, etc. 

![image](https://user-images.githubusercontent.com/78588391/212954775-68950203-497d-437b-9d17-4587a7b812ba.png)

#### C'est apres le "tasks:" que les taches se deploient et executent leurs actions. 
1. name: Description simple de la tache
2. Un module. Ce qui vient apres sont les parametres du module. 
3. Pour la seconde tache ---> script: indique que c'est un script qui vas s'executer.  
(le script en question) 

![image](https://user-images.githubusercontent.com/78588391/212956562-8c69600d-78d2-41a7-9aaf-b818a09d6010.png)

## Un peu plus sur Ansible: Les roles

Les rôles fournissent un cadre et une structure bien définis pour définir nos tâches, variables, gestionnaires, métadonnées, modèles et autres fichiers. Ainsi, nous pouvons les référencer et les appeler dans nos playbooks avec seulement quelques lignes de code, tandis que nous pouvons réutiliser les mêmes rôles sur de nombreux projets sans avoir à dupliquer notre code.

Je vais montrer comment le fonctionnement des roles en installent Nginx webserver et en remplacent la page par default de Nginx sous debian par une page personnelle.
> Structure de notre role:
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2009-40-19.png)

1. default va contenire des variables.
2. handlers: Sont des taches speciales qui se seront actives que via la directive "notify".
3. tasks: Ensemble de nos taches qui se deploierons sur les machines hosts.
4. templates: Permet de crer des nouveaux fichiers au format jinja2.

> Contenue du fichier tasks: 
  ![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2009-49-01.png)
  
  "Replace default page" va modifier la page html par default en prenant pour source index.html.j2, la page personnalise.
 
 > Les differentes variables qui peuvent etres appelles au seins de notre role:
 
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-07-08.png)

Pour appeller l'une de ces variables utiliser la syntax: "{{ **nom_de_variable** }}", qui seront souvent appeller dans tasks.

De cette maniere, notre page par default sera modifier de cetter maniere: 

![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-06-51.png)

**__cliquer pour voir le deploiement du roles__**
[![asciicast](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2010-58-16.png)](https://asciinema.org/a/SgPUVITOapHD1PwHm0kFlAqMP)
Les options -DC: 
1. Pour montrer la difference dans les fichiers de configuration et lors de l'execution des taches.
2. C Pour lancer le playbook en mode check. Cela ne va que simuller les changements, telechargements et mises en place des paquets par exemple etc. Option tres utile pour faire des tests et s'assurer que tout fonctionne bien. 

Il y a une "erreur" a la fin car le playbook essaye de simulier le redemarage d'un service, nginx... Ce n'est pas possible, soit le service redemarre, soit il ne redemmare pas :)

[![asciicast](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-02-06%2011-10-32.png)](https://asciinema.org/a/3sdVrff6tMoYslks06SHuqmO5)

#### A suire...

# Lab reseau
Il m'a par la suite ete donne un lab a faire et a deploiyer, qui m'a permit de travailler sur plusieurs aspects reseaux.
Nous trouverons un client installee sous ![RockyLinux](https://rockylinux.org/), et un serveur hebergent differents services web sous Debian. Les deux se trouvant sur des reseaux differents. En intermediaire, un pare-feu logiciel pfSense permettra le routage et le filtrage des connections entre les deux reseaux.
Ci-dessous un schema du lab en question a mettre en place:

![lien du lab](https://github.com/JuiceMcgoose/assets/blob/main/lab_reseau_mehdi.drawio.png) 

### Mise en place des differentes machines sous le noeud proxmox:
Il sera tout d'abord question de configurer nos differentes machines pour qu'elles puissent communiquer entre elles.
> Notre noeud proxmox se trouve sous le reseau **172.30.112.0/24** sa gw en **172.30.112.0.254**
Le client recoit automatiquement une ip(172.30.112.191) dans ce reseau via dhcp.

Le pfSense devra avoir deux interfaces, une dans chaques reseaux. L'ip par defaut de l'interface pfSense qui nous permet d'acceder a l'interface web est 192.168.1.1, or, notre serveur dans le reseau 10.8.0.0/24, il faudra egallement changer cela.

Configuration finales des interfaces pfsense.
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2011-43-40.png)

Il faudra mettre en place une nouvelle route sur chacunes des machines pour permettre la communication vers les differentes interfaces de notre pare-feu.
Pour notre reseau Lan, c'est simple, celui-ci ne dispose que d'une seule rouete possible. Pour notre reseau Wan en revange, deux chemins de transports sont disponibles, l'un en direction du Lan, l'autre en direction du proxmox et du reseau externe. 

> Routage serveur
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2014-15-19.png)

> Routage client
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2014-14-22.png)

> Passage des paquets
![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2017-43-57.png)

### Mise en place des regles de pare-feu

Dans notre scenarios, notre client doit contacter le server pour acceder a certains services. Objectif: uniquement authoriser la connection a ces services, et depuis ce client uniquement. Nous mettrons en place certaines regles de pare-feu ayant ces effets. 

Les regles a mettre en place: 

> 1. Apache via les ports 80/443
> 2. MariaDB via le port 3309
> 3. SSH via le port 22 
> 4. Bloquer tout autre connections 


![](https://github.com/JuiceMcgoose/assets/blob/main/Screenshot%20from%202023-01-31%2017-04-24.png)

## Fail2ban

Fail2ban agit a une couche differente de la couche reseau de niveau 3 d'un pare-feu. Celui-ci bloque les paquets du protocol tcp. Mais le port 22 est encore ouvert et des connections peuvent toujours avoir lieux. C'est la que rentre en jeu le logiciel Fail2ban en suiveillant les entrees des logs de no services. Fail2ban offre de nombreuses options pour securiser notre serveur, pour limiter les attaques par brutes-force ou DDOS.
Les parametres a prendre en compte:
1. bantime 10m (definie la duree du bannisement)
2. findtime 2m (fourchette de temps pendant laquelle les tentatives de connections ammenent a un bannisement)
3. maxretry 3 ( nombre de tentatives maximum)
4. ssh = yes ( s'applique sur ssh )


## Firewalld
...







