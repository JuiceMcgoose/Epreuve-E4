# Stage
## Here I will be describing the different projects et thechnologies I worked on during my internship.

### Here is a link to a screenshot: [e](https://imgur.com/gallery/zPFhSqy)
Some quotes:
> Nice!

![Screenshot from 2023-01-17 14-21-29](https://user-images.githubusercontent.com/78588391/212909851-db257362-4e3b-4d5a-b2b6-40574b4e2fb5.png)


# Working with Ansible: 
[lien pour 'become'](https://www.digitalocean.com/community/tutorials/understanding-privilege-escalation-in-ansible-playbooks)

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


#### A suire...

# Lab reseau
Il m'a par la suite ete donne un lab a faire et a deploiyer, qui m'a permit de travailler sur plusieurs aspects reseaux.
Nous trouverons un client installee sous ![RockyLinux](https://rockylinux.org/), et un serveur hebergent differents services web sous Debian. Les deux se trouvant sur des reseaux differents. En intermediaire, un pare-feu logiciel pfSense permettra le routage et le filtrage des connections entre les deux reseaux.
Ci-dessous un schema du lab en question a mettre en place:

![lien du lab](https://github.com/JuiceMcgoose/assets/blob/main/lab_reseau_mehdi.drawio.png) 

### Mise en place des differentes machines sous le noeud proxmox:
Il sera tout d'abord question de configurer nos differentes machines pour qu'elles puissent communiquer entre elles.
> Notre noeud proxmox se trouve sous le reseau **172.30.112.0/24** sa gw en **172.30.112.0.254**
Le client recoit automatiquement une ip dans ce reseau via dhcp.

Le pfSense devra avoir deux interfaces, une dans chaques reseaux. L'ip par defaut du pfSense qui nous permet d'acceder a l'interface web est 192.168.1.1, or, notre serveur dans le reseau 10.8.0.0/24, il faudra egallement changer cela.



