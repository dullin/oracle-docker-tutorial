# Installation de Docker

Vous pouvez suivre la documentation d'installation en anglais au [lien suivant](https://docs.docker.com/docker-for-mac/install/).

Télécharger Docker du [lien suivant](https://download.docker.com/mac/stable/Docker.dmg) et installer là dans votre dossier d'application.

À sa première exécution, docker va vous demander d'installer ses outils.

![](whale-in-menu-bar.png)

Docker est prêt-à être utiliser quand son icône n'est plus animer, vous pouvez aussi regarder son étant en cliquant sur l'icône.

![](docker-running.png)

# Installation de SQL Developer

SQL Developer est disponible au [lien suivant](https://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html).

Faire attention, la version de java JDK8 d'oracle doit être installée avant de pouvoir utiliser SQL Developer. Ci ce n'est pas déjà installé, vous pouvez vous le procurer [sur le site d'Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Une fois téléchargé, copiez l'application dans votre dossier d'Application.

# Installation de la base de données Oracle 11g sur Docker

Ouvrez le terminal et exécutez la commande suivante:
```
docker run --name oracle11g -d -p 1521:1521 wnameless/oracle-xe-11g
```

Cela va installer et configurer la base de données sur votre système.

# Connexion et création d'utilisateurs avec SQL Developer

Il faut faire une première connexion avec le compte `system` pour se créer un utilisateur normal pour notre base de données.

Ouvrez SQL Developer et faite une nouvelle connexion.

![](sql-connect.png)

Entrez les informations suivantes :
```
Connection name : À votre choix
Username : system
Password : oracle
```

![](login-info.png)

Appuyez sur `connect` pour se connecter à la base de données.

La première connexion avec le compte système sera temporaire pour créer le compte utilisateur normal.

Avec la connexion établie, vous serez accueilli par la fenêtre de script à envoyer à notre base de données. Nous l'utiliserons pour ajouter un nouvel utilisateur.

```SQL
create user nomUsager identified by monMotDePasse;
grant connect, resource to nomUsager;
```

Où le `nomUsager` et `monMotDePasse` est de votre propre crue.

![](create-user.png)

On exécute le script en cliquant sur le bouton `Run script` ou en pesant sur F5.

Si tout a bien été, la fenêtre d'affichage de script nous indique que le compte est créé et que les accès sont accordés.

![](create-success.png)

Avec la création de notre compte, nous allons modifier les informations d'accès pour nous connecter à partir de notre compte à l'instar du compte system.

Avec un clic droit sur le serveur, on peut changer les `properties` qui nous ramène aux informations de connexions. Nous allons changer les informations pour le nouveau compte créé.

![](new-user.png)

Avec cela, nous pouvons nous connecter et utiliser la base de données sur macOS.

# Fermeture et reouverture de la base de données
Vous pouvez quitter docker à partir de la barre de menu pour fermer la base de données quand elle n'est pas utilisée.

Pour repartir la base de données, il faut:

* Repartir l'application Docker et attendre qu'elle soit initialisée (pas d'animation dans l'icône)
* Ouvrir le terminal et taper la commande suivante :
```
docker start oracle11g
```

Cela va repartir la base de données et vous pourrez vous connecter à celle-ci à partir de SQL Developer.
