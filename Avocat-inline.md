![alt_tag](https://user-images.githubusercontent.com/60784585/74037024-bc003c00-49bd-11ea-922a-a960fb343dcf.png)

# Projet linux

Avoca Inline

BRANAS Jeremy | Linux | 29/01/2020

# Introduction :

Dans le cadre de ma formation au cesi je dois réaliser un projet baser sur linux, pour ce projet je dois réaliser une infrastructure et une documentation d’installation.

# Rappel du sujet :

SUJET LINUX – soutenance 5/6 février 2020 (Restitution du dossier une semaine à l’avance)

La société « Avocat Inline » compte 20 avocats, leur service administratif et commercial de 5 personnes. Cette société souhaite consolider et étendre son réseau professionnel et sa clientèle. Pour cela elle doit investir dans son infrastructure informatique.

La société n'a pas beaucoup de moyens et surtout elle veut utiliser des logiciels libres. Afin de répondre à sa demande, elle est à la recherche d’une équipe IT qui pourrait les aider à :

-  Installer un SI stable, robuste et résilient (données sécurisées et sauvegardées),

-  Les accompagner dans ce changement

-  Prévoir une exploration simple et peu onéreuse L'infrastructure aura deux parties LAN/WAN :

## Infrastructure LAN :

1.  Un serveur DNS : ce serveur aura pour but de faire les résolutions DNS sur le réseau local de l'entreprise

2.  Un serveur intranet : Solution WordPress

3.  Un serveur de base de données qui hébergera la BDD du WordPress

4.  Un serveur annuaire : permettra l'authentification sur le serveur intranet

5.  Un serveur qui stockera les sauvegardes

6.  Un reverse proxy pour accéder au WordPress depuis le réseau utilisateur

7.  Aucun serveur du réseau local n'aura pas accès à internet ; les dépôts seront stockés sur un serveur qui gérera le cache (à configurer dans les sources.list des différents serveurs)

8.  Utilisation d'un outil de provisionnement. La solution sera supervisée :

## La partie WAN comportera :

1.  Une passerelle de sortie vers internet

2.  Un serveur qui permettra l'externalisation des sauvegardes (facultatif)

## Supervision :

1.  Une solution capable de superviser la partie LAN/WAN (pas de supervision des terminaux)

2.  Avoir des métriques

3.  Avoir des alertes

4.  Automatisation d'actions mineures (facultatif)

## Sécurisation :

Mettre en place des solutions permettant de sécuriser les éléments d’infrastructure :

1. LDAP

2. DNS

3.HTTP

4.BDD

## Résumé des services

### Minimum attendu

1.  DNS

2.  LDAP

3.  DHCP

4.  BDD

5.  WEB

6.  NFS

7.  SSH (serveur rebond)

8.  Sauvegarde

9.  Gestion de configuration (implique que l'on pourra redéployer la configuration d'un serveur Web si celui-ci venait à planter.)

### Services optionnels

1.  Fail2ban

2.  Reverse Proxy

3.  OSSEC

4.  Supervision/métrologie

5.  Ansible

6.  SpaceWalk

7.  Docker

# Présentation des Outils :

Pour la virtualisation j’ai utilisé vmware qui permet de créer des vm  ( virtual machine ) :

![alt_tag](https://user-images.githubusercontent.com/60784585/74037363-62e4d800-49be-11ea-8399-27131f040389.png)

Pour les serveurs j’ai utilisé Debian 10 comme os :

![alt_tag](https://user-images.githubusercontent.com/60784585/74037519-ba834380-49be-11ea-97fe-b6471837ccf4.png)

Pour le serveur de base de donner j’ai utilisé mariadb :

![alt_tag](https://user-images.githubusercontent.com/60784585/74037639-f74f3a80-49be-11ea-83e9-edf306c32a2f.png)

Pour le serveur WEB j’ai utilisé Wordpress :

![alt_tag](https://user-images.githubusercontent.com/60784585/74037776-439a7a80-49bf-11ea-9480-ab4dde37e997.png)

Pour le firewall j’ai utilisé PFsense :

![alt_tag](https://user-images.githubusercontent.com/60784585/74037910-8d836080-49bf-11ea-8e4e-2ca7426a8e53.png)

Pour le serveur de monitoring j’ai utilisé Zabbix :

![alt_tag](https://user-images.githubusercontent.com/60784585/74038031-c4f20d00-49bf-11ea-9b8c-d21028aae80f.png)

Pour les machines client j’ai utilisé Windows 10 comme os :

![alt_tag](https://user-images.githubusercontent.com/60784585/74038120-f074f780-49bf-11ea-82ce-57835f4137ab.png)

Pour le serveur de sauvegarde j’ai utilisé Windows serveur 2016 :

![alt_tag](https://user-images.githubusercontent.com/60784585/74038277-316d0c00-49c0-11ea-82fc-b9f250025c35.png)

Pour le serveur de sauvegarde j’ai utilisé Veeam :

![alt_tag](https://user-images.githubusercontent.com/60784585/74038397-6a0ce580-49c0-11ea-9bad-b35d3374d804.png)


Pour le serveur de fichiers j’ai choisi :

![alt_tag](https://user-images.githubusercontent.com/60784585/74038525-a8a2a000-49c0-11ea-83fc-0ec9aa205dd6.png)


Pour le serveur LDAP j’ai choisi Zentyal qui fonctionne sous Ubuntu :

![alt_tag](https://user-images.githubusercontent.com/60784585/74038676-dbe52f00-49c0-11ea-920b-e628ac4ea956.png)


Le choix des différents outils est principalement du au fait qu’il soit gratuit pour la grande majorité et donc pouvoir respecter le budget limité de la société avocat Inline ainsi qu'en open-source se qui donne une bonne visibilité sur la solution.

Le choix du serveur de sauvegarde avec un os Windows et veeam n’est quant à lui pas financier puisque Windows et veeam sont payant, mon choix c’est fait sur la fiabilité et le coté pratique de la solution veeam ainsi que sur le support veeam qui est efficace.

Le choix d’utiliser Zentyal pour le serveur LDAP comme solution car elle est plus simple et de manière générale plus compatible avec d'autre solution,os... que par exemple SAMBA en mode contrôleur de domaine.


# Présentation de l’infrastructure :

![alt_tag](https://user-images.githubusercontent.com/60784585/74039243-ca505700-49c1-11ea-95a7-db1ac6e8b13f.png)


Nous avons des vm connecter en lan et un firewall connecter sur le lan et sur un wan (SRV-VM-FW-001) non représenter sur l'image au-dessus.

Les rôles et fonctions sont donc réparties sur plusieurs serveurs qui seront des vm.

Une vm vas être lADP, DNS, DHCP.

Une vm seras le serveur web.

Une vm seras le serveur bdd.

Une vm sera le serveur de monitoring

Une vm seras le firewall.

Le serveur de sauvegarde lui est appart et il est physique et non pas en vm. (pour la maquette il sera une vm).


## Le nommage :

Les différents équipements vont être soumis à des règles de nommage.

Pour un server on aura : SRV-nomserveur-id

Pour une vm on aura : SRV-VM-nomvm-id

L’id correspond au numéro du serveur ou de la vm, exemple s’il y a plusieurs AD on va les numéroter de 001 à 999.

Dans notre cas :

Le serveur AD SRV-VM-AD-001 et le secondaire SRV-VM-AD-002

Le serveur de base de données SRV-VM-BDD-001 et le secondaire SRV-VM-BDD-002

Le serveur web SRV-VM-WEB-001 et le secondaire SRV-VM-WEB-002

Le serveur de monitoring SRV-VM-MNT-001 et le secondaire SRV-VM-MNT-002

Le firewall SRV-VM-FW-001 et le secondaire SRV-VM-FW-002

Le serveur de sauvegarde SRV-BACKUP

Le serveur NFS sera SRV-VM-FS-001

Le domaine sera inline.cesi


## Présentation de l’infrastructure réseaux :

(Le schéma représente une infrastructure réseaux théorique dans l’entreprise avocat Inline et non celle de la maquette)

![alt_tag](https://user-images.githubusercontent.com/60784585/74039884-eef8fe80-49c2-11ea-910b-8f178d09b474.png)


Pour le projet j’ai défini 3 sous réseaux LAN : 192.168.10.0  30.0  20.0.

Les adresses en 192.168.10.0 seront pour les serveurs.

Les adresses en 192.168.20.0 seront pour le matériel (imprimante…).

Les adresses en 192.168.30.0 seront pour les pc utilisateurs.

Le WAN lui sera 192.168.1.0


# Installation Debian 10 :

Au lancement de l’installation, il est proposé plusieurs options. On choisit la premier « Install »

![alt_tag](https://user-images.githubusercontent.com/60784585/74040247-9ece6c00-49c3-11ea-8527-8377cc8ec56c.png)

Ensuite, il est demandé de choisir un nom pour ce système :

Il faut donc rentrer le nom du serveur que l’on veut créer, exemple : SRV-VM-AD-001.

![atl_tag](https://user-images.githubusercontent.com/60784585/74040332-ccb3b080-49c3-11ea-8b5a-76125641bf37.png)

L’étape suivante nous demande de saisir un domaine si l’on souhaite intégrer cette machine dans un domaine existant. Si ce n’est pas le cas laisser le champ vide, on pourra par la suite intégrer notre serveur a un domaine.

![alt_tag](https://user-images.githubusercontent.com/60784585/74040433-01276c80-49c4-11ea-816c-eaf06024b2c9.png)

Saisissez ensuite un mot de passe pour le compte « root » du système ( root est le compte Administrateur de la machine, il a tous les droits ), il faut choisir un mot de passe suffisamment complexe.

![alt_tag](https://user-images.githubusercontent.com/60784585/74040533-2e741a80-49c4-11ea-899c-880eef5b814b.png)

Une confirmation est demandée il faut donc re taper le même mot de passe.

![alt_tag](https://user-images.githubusercontent.com/60784585/74040662-68452100-49c4-11ea-8019-6ed0bdde26fd.png)

La prochaine étape demande un identifiant pour un compte utilisateur du système ainsi que son mot de passe, exemple l’utilisateur s’appelle valentin :

![alt_tag](https://user-images.githubusercontent.com/60784585/74040745-9d517380-49c4-11ea-89e8-3e8ac1fc2ac2.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74040797-ba864200-49c4-11ea-83ee-838976230d94.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74040896-ea354a00-49c4-11ea-9d89-07ccbf38b181.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74040958-06d18200-49c5-11ea-8683-9806932f6bbc.png)


La prochaine étape est importante, il s’agit du partitionnement du disque. Pour ma part, j’ai choisi les paramètres recommandés :

![alt_tag](https://user-images.githubusercontent.com/60784585/74041051-35e7f380-49c5-11ea-8a4e-ef38aa18eaad.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74041106-52842b80-49c5-11ea-9495-33d861a7736f.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74041178-78113500-49c5-11ea-90ac-6c52f8714fcc.png)

On pourra par la suite créer des disques et leur attribuer une taille si on le souhaite.

![alt_tag](https://user-images.githubusercontent.com/60784585/74041327-bd356700-49c5-11ea-8524-b3ded1247bf1.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74041386-d8a07200-49c5-11ea-8456-180ad5ceb29c.png)

Ensuite, il va être demandé un site pour télécharger les Paquets, il s’agit d’un endroit où sont stockés tous les fichiers systèmes, les Appliances, etc …

![alt_tag](https://user-images.githubusercontent.com/60784585/74041499-0b4a6a80-49c6-11ea-9627-3c2679a447c8.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74041569-2ae19300-49c6-11ea-9f02-4ffad5ec0325.png)

S’il y a un proxy, il est demandé dans la fenêtre suivante si ce n’est pas le cas laisser le champ vide.

![alt_tag](https://user-images.githubusercontent.com/60784585/74041627-4ea4d900-49c6-11ea-9576-e30fe210c9db.png)

La prochaine fenêtre, propose les logiciels prédéfinis à installer, pour cette installation aucun logiciel n’est utile sauf « utilitaire usuel du système » comme chaque fois on pourra rajouter de fonctionnalités par la suite.

![alt_tag](https://user-images.githubusercontent.com/60784585/74041742-83b12b80-49c6-11ea-993a-22aa281ae794.png)

Le système « GRUB » qui permet l’amorçage du système est demander ensuite. Il est fortement recommandé de l’installer.

![alt_tag](https://user-images.githubusercontent.com/60784585/74041874-c410a980-49c6-11ea-8db1-cae4df23cff4.png)

Choisir le disque ou le secteur d’amorçage sera installer :

![alt_tag](https://user-images.githubusercontent.com/60784585/74041967-f6220b80-49c6-11ea-8aed-536d2f00faae.png)

Le système va ensuite redémarrer et fonctionnel. (Si vous travaillez sur une machine virtuelle, il est recommandé de faire un snapshot de la machine pour revenir en arrière en cas de problème).

## Paramétrage d’une ip static :

Le fichier contenant les adresses IP de chaque carte réseau se trouve dans le fichier interfaces.

	nano /etc/networck/interfaces/

Le fichier se trouve sous la forme suivante :

![alt_tag](https://user-images.githubusercontent.com/60784585/74042268-7d6f7f00-49c7-11ea-9f1f-5fa72bb7051f.png)

On le modifie avec l’adresse qu’on veut :

![alt_tag](https://user-images.githubusercontent.com/60784585/74042354-a728a600-49c7-11ea-9af4-f9dabc9769db.png)

## Installation du module SSH :

Pour pouvoir se connecter en ssh sur un serveur il faut installer le module :

	apt-get install openssh-server 

![alt_tag](https://user-images.githubusercontent.com/60784585/74042485-e8b95100-49c7-11ea-8282-d06c77739413.png)

A cette étape on tape O pour continuer l’installation.

Pour tester la connexion SSH on peut utiliser Putty qui est un logiciel fait pour la connexion SSH .

![alt_tag](https://user-images.githubusercontent.com/60784585/74042612-25854800-49c8-11ea-9abe-93e1fee0f9ce.png)

On rentre l’ip du serveur sur lequel on vient d’installer le module :

![alt_tag](https://user-images.githubusercontent.com/60784585/74042693-52d1f600-49c8-11ea-88c3-a22655aca508.png)

Puis on rentre l’user : (ATTENTION : l’user root est par défaut bloquer en ssh il faut don utiliser l’utilisateur basique défini lors de l’installation de linux ou un autre user autoriser en ssh) :

![alt_tag](https://user-images.githubusercontent.com/60784585/74042803-7e54e080-49c8-11ea-8891-3553e88bafd6.png)

Puis pour passer en root :

![alt_tag](https://user-images.githubusercontent.com/60784585/74042881-a17f9000-49c8-11ea-8f7b-e0a793953a01.png)

On peut constater que l’on est bien passé en root :

![alt_tag](https://user-images.githubusercontent.com/60784585/74042958-cc69e400-49c8-11ea-8534-7803f3eafe51.png)


