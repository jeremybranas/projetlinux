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


# Installation ZABBIX :

Pour installer zabbix il nous faut une vm sous Debian

Installer apache et php :

![alt_tag](https://user-images.githubusercontent.com/60784585/74157891-645e0c80-4c19-11ea-89bd-4a1772a8507f.png)

Vérifier que le service apache est actif :

![alt_tag](https://user-images.githubusercontent.com/60784585/74158025-a12a0380-4c19-11ea-9a41-a779ab2df5be.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74158084-bc950e80-4c19-11ea-88db-4261bc199b54.png)

Se rendre sur le serveur SRV-VM-BDD-001

Se connecter à la base mariadb :

![alt_tag](https://user-images.githubusercontent.com/60784585/74158174-e4847200-4c19-11ea-8fef-e7bdb6efc027.png)

Créer la base zabbix et l’utilisateur en full privilège zabbix :

![alt_tag](https://user-images.githubusercontent.com/60784585/74158278-172e6a80-4c1a-11ea-8377-d98e9ab529ba.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74158349-36c59300-4c1a-11ea-8e0f-53f7bac07cb8.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74158398-4ba22680-4c1a-11ea-8a65-94105b194877.png)

On ajoute les lignes suivante dans : /etc/mysql/mariadb.conf.d :
![alt_tag](https://user-images.githubusercontent.com/60784585/74158498-77bda780-4c1a-11ea-9f19-c54d3b82c3bc.png)

On repart sur le serveur SRV-VM-MNT-001 et on install zabbix :

![alt_tag](https://user-images.githubusercontent.com/60784585/74158568-991e9380-4c1a-11ea-878b-ff97b13adb6d.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74158622-b0f61780-4c1a-11ea-9e3e-7aa2f0818adc.png)
On install les packages pour l’interface web :

![alt_tag](https://user-images.githubusercontent.com/60784585/74158715-d8e57b00-4c1a-11ea-9592-debdec982fd2.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74158768-f1559580-4c1a-11ea-9853-20c3bcfea355.png)

On configure le fichier de conf zabbix :

![atl_tag](https://user-images.githubusercontent.com/60784585/74158844-1518db80-4c1b-11ea-9d8a-92bc30e7341c.png)

On remplace par nos valeurs :

![alt_tag](https://user-images.githubusercontent.com/60784585/74159027-5a3d0d80-4c1b-11ea-973c-c603ee15bc1e.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74159089-76d94580-4c1b-11ea-9d01-d907cbf78236.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74159228-b6079680-4c1b-11ea-94c5-1c75ebb9f60c.png)![amt_tag](https://user-images.githubusercontent.com/60784585/74159269-c9b2fd00-4c1b-11ea-8dcb-1d1da4050ffa.png)

On va configurer le fichier de configuration php pour que ça fonctionne avec l’interface zabbix, on va paramétrer le bon fuseau horaire.

![alt_tag](https://user-images.githubusercontent.com/60784585/74159371-f830d800-4c1b-11ea-9b26-c4d7e5ea95fb.png)
Enlever le # de : php_value date.timezone Europe/Riga

![alt_tag](https://user-images.githubusercontent.com/60784585/74159460-1f87a500-4c1c-11ea-982f-de399f4fe02a.png)

On redémarre le service :
![alt_tag](https://user-images.githubusercontent.com/60784585/74159618-5b226f00-4c1c-11ea-8d75-05fa600d74e8.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74159725-85742c80-4c1c-11ea-92e5-2f0046552df8.png)	

On va configurer zabbix depuis l’interface web, on va utiliser google chrome : [http://192.168.10.247/zabbix/setup.php](http://192.168.10.247/zabbix/setup.php)

![alt_tag](https://user-images.githubusercontent.com/60784585/74159806-a89edc00-4c1c-11ea-9c38-4c5c6d295d4a.png)

Cliquer sur next setup , bien vérifier que tout est ok :

![alt_tag](https://user-images.githubusercontent.com/60784585/74159917-dc7a0180-4c1c-11ea-8adf-8dfc36575408.png)

Cliquer sur next, on va configurer l’accès à la bdd : (on met le port 3306 c'est le port par default pour la bdd)	


![alt_tag](https://user-images.githubusercontent.com/60784585/74160050-164b0800-4c1d-11ea-87f7-22626a63b755.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74160134-3975b780-4c1d-11ea-8b3e-5fc4114a5642.png)![alt_tag](https://user-images.githubusercontent.com/60784585/74160184-527e6880-4c1d-11ea-9799-13d0735e17df.png)

La configuration initiale de l’interface est finie :

Maintenant on se connecte : identifiant : Admin mdp : zabbix :

Puis se rendre dans administration, user pour changer la langue et le mot de passe :

![alt_tag](https://user-images.githubusercontent.com/60784585/74160293-7641ae80-4c1d-11ea-8166-a125ad900b94.png)

Il suffit ensuite de paramétrer le monitoring :

Pour se connecter utiliser l’url : [http://192.168.10.247/zabbix](http://192.168.10.247/zabbix).

![alt_tag](https://user-images.githubusercontent.com/60784585/74160447-b86af000-4c1d-11ea-9fc6-488fd361df4d.png)
![alt_tag](https://user-images.githubusercontent.com/60784585/74160505-cf114700-4c1d-11ea-8735-09d62b3f91a5.png)


# Installation de wordpress :

Pour installer wordpress il nous faut une vm avec débian.

Installer Apache sur Ubuntu Linux

WordPress nécessite un serveur Web avec support PHP pour présenter ses pages Web.

Utilisez la commande Ubuntu APT pour installer le serveur Apache.

    apt-get update  
	apt-get install apache2 php7.2 php7.2-mysql libapache2-mod-php7.2  
	service apache2 restart

Utilisez la commande suivante pour installer les modules PHP les plus utilisés d’Apache 7.2 ou 7.3 etc.

	apt-get install php7.2-xml php7.2-curl php7.2-gd php7.2-mbstring  
	 apt-get install php7.2-bz2 php7.2-zip php7.2-xml php7.2-curl  
	apt-get install php7.2-json php7.2-opcache php7.2-readline

Utilisez la commande suivante pour activer apache mod_rewrite et SSL.

Activez le module SSL uniquement si vous envisagez de proposer du contenu HTTPS.

	 a2enmod rewrite  
	 a2enmod ssl  
	 service apache2 restart

Recherchez l'emplacement du fichier de configuration PHP sur votre système.

Editez le fichier de configuration php.ini.

![alt_tag](https://user-images.githubusercontent.com/60784585/74160847-52cb3380-4c1e-11ea-8bf0-50f0e1eec9ae.png)
Et mettre cette config :
![alt_tag](https://user-images.githubusercontent.com/60784585/74160930-70989880-4c1e-11ea-81e6-d58d9e239a2e.png)

Redémarrez le serveur Web Apache manuellement.

	service apache2 restart
	service apache2 status

![alt_tag](https://user-images.githubusercontent.com/60784585/74161033-a047a080-4c1e-11ea-9cf6-31ceafcc570e.png)

Téléchargez la dernière version de WordPress et extrayez-le package.

	wget https://wordpress.org/latest.tar.gz  
	tar -zxvf latest.tar.gz

Déplacez le dossier WordPress dans votre répertoire de lecteur racine Apache.

Donnez à l'utilisateur www-data le contrôle total sur le répertoire WordPress et ses fichiers.

	mv wordpress /var/www/html/  
	chown www-data:www-data /var/www/html/wordpress/* -R

Créez et éditez le fichier de configuration WordPress wp-config.php.

	cd /var/www/html/wordpress  
	mv wp-config-sample.php wp-config.php  
	vi wp-config.php

Modifiez les informations de connexion à la base de données MySQL situées sur le fichier wp-config.file.

A titre d'exemple, voici le fichier avec notre configuration.


