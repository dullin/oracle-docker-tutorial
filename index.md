[Playlist Youtube pour l'installation](https://www.youtube.com/playlist?list=PLliSmgNDYPxyO0qZ0yefbOHA5TbhDMOkj)

# Installation de Docker

Vous pouvez suivre la documentation d'installation en anglais au [lien suivant](https://docs.docker.com/docker-for-mac/install/).

Téléchargez l'application Docker du [lien suivant](https://download.docker.com/mac/stable/Docker.dmg) et installez-la dans votre dossier d'applications.

À sa première exécution, Docker demandera la permission d'installer ses outils. Votre mot de passe d'administrateur sera nécessaire.

![](whale-in-menu-bar.png)

Docker est prêt lorsque son icône n'est plus animé. Vous pouvez aussi consulter son état en cliquant sur l'icône.

![](docker-running.png)

# Installation de SQL Developer

SQL Developer est disponible au [lien suivant](https://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html).

Faites attention, la version de Java JDK8 d'Oracle doit être installée avant de pouvoir utiliser SQL Developer. Si elle n'est pas déjà installée, vous pouvez vous la procurer [sur le site d'Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Une fois téléchargée, copiez-la dans votre dossier d'applications.

# Installation de la base de données Oracle 11g sur Docker

Ouvrez un terminal et exécutez la commande suivante:
```
docker run --name oracle11g -d -p 1521:1521 wnameless/oracle-xe-11g
```

Cela va installer et configurer une base de données sur votre système.

# Connexion et création d'un utilisateur avec SQL Developer

Il faut faire une première connexion avec le compte `system` pour créer un utilisateur normal sur votre base de données.

Ouvrez SQL Developer et créez une nouvelle connexion.

![](sql-connect.png)

Entrez les informations suivantes :
```
Connection name : À votre choix
Username : system
Password : oracle
```

![](login-info.png)

Appuyez sur `connect` pour vous connecter à la base de données.

La première connexion avec le compte système est temporaire et ne sert qu'à créer le compte utilisateur normal.

Une fois la connexion établie, vous serez accueilli par la fenêtre de script à envoyer à la base de données. Nous l'utiliserons pour ajouter un nouvel utilisateur.

```SQL
create user nomUsager identified by monMotDePasse;
grant connect, resource to nomUsager;
```

où vous pouvez choisir le `nomUsager` et `monMotDePasse`.

![](create-user.png)

Exécutez le script en cliquant sur le bouton `Run script` ou appuyez sur F5.

Si tout a bien été, la fenêtre d'affichage de script indiquera que le compte est créé et que les accès sont accordés.

![](create-success.png)

Maintenant que votre compte a été créé, nous allons modifier les informations d'accès pour vous reconnecter à partir de votre compte plutôt qu'avec le compte système.

Avec un clic droit sur le serveur, sélectionnez `properties` qui vous ramène aux informations de connexion. Nous allons changer les informations pour celles du nouveau compte créé.

![](new-user.png)

Ainsi, vous pouvez vous connecter et utiliser la base de données sur macOS.

# Fermeture et réouverture de la base de données
Pour fermer la base de données quand elle n'est pas utilisée, vous pouvez quitter Docker à partir de la barre de menu.

Pour réouvrir la base de données :

* Relancez l'application Docker et attendez qu'elle soit initialisée (pas d'animation dans l'icône)
* Ouvrir le terminal et tapez la commande suivante :
```
docker start oracle11g
```

La base de données sera prête pour utilisation et vous pourrez vous connecter à celle-ci à partir de SQL Developer.
