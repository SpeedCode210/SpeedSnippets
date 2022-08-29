# Utilisation de LSAM

LSAM est un utilitaire en ligne de commande permettant de gérer des applications serveur utilisant NodeJS, .NET, Go, Python et plein d'autres, et ce en créant et gérant automatiquement des services systemd.

Pour l'installer, vous pouvez télécharger le paquet compatible avec votre distribution sur [GitHub](https://github.com/SpeedCode210/lsam/) depuis la dernière release.

**NB :** Dans la version actuelle de LSAM, toutes les commandes doivent être exécutées en tant que  `root`.

## Ajout d'une application

1) Utilisez la commandes `lsam create` et suivez l'assistant, voici l'exemple pour une application Node.JS :
  
```n
[root@fedora-raouf ~]# lsam create
N.B. Please install before launching the necessary runtimes/compilers for your app.
Please enter application name : App1
Please choose the type of the app : 
1) .NET
2) NodeJS
3) Golang
4) Java
5) Python
6) Lua
7) Rust (Cargo)
8) Custom command
2
Does your application need root permissions ? [y/N]n
Please enter the file (command if custom command selected) to run with needed args. [index.js] app.js 
Created symlink /etc/systemd/system/multi-user.target.wants/app1.service → /etc/systemd/system/app1.service.
The application has been created, please go to the folder of the app with this command :
'cd /home/lsam/applications/app1' to put in it the application's files
Then start it using the command : 'lsam start app1'
```

2) Placez les fichiers de l'application via SFTP, Git, ou autre dans le dossier indiqué par LSAM (En l'occurence `/home/lsam/applications/app1`).
   
3) Démarrez l'application via la commande `lsam start app1` en remplaçant `app1` par le nom de votre application.

## Affichage d'informations

- Lister les applications sur la machine avec la commande `lsam list`:
```n
[root@fedora-raouf ~]# lsam list
┌────────┬───────────┬───────────┬─────────────┬─────────────┐
│  Name  │  Service  │  Status   │  Autostart  │  Root       │
├────────┼───────────┼───────────┼─────────────┼─────────────┤
│  App1  │  app1     │  Stopped  │  Yes        │  No         │
└────────┴───────────┴───────────┴─────────────┴─────────────┘
```

- Affichage des informations d'une application avec la commande `lsam info <app>`:
```n
[root@fedora-raouf ~]# lsam info app1
┌───────────────┬────────────────────────────────┐
│  Application  │  App1                          │
├───────────────┼────────────────────────────────┤
│  Service      │  app1.service                  │
├───────────────┼────────────────────────────────┤
│  Main file    │  app.js                        │
├───────────────┼────────────────────────────────┤
│  Type         │  NodeJS                        │
├───────────────┼────────────────────────────────┤
│  Directory    │  /home/lsam/applications/app1  │
├───────────────┼────────────────────────────────┤
│  Autostart    │  Yes                           │
├───────────────┼────────────────────────────────┤
│  Root         │  No                            │
├───────────────┼────────────────────────────────┤
│  Status       │  Stopped                       │
└───────────────┴────────────────────────────────┘
```

## Démarrage/Arrêt des applications

- Démarrer une application :
```n
lsam start <app>
```

- Redémarrer une application :
```n
lsam restart <app>
```

- Arrêter une application :
```n
lsam stop <app>
```

- Tuer le processus une application :
```n
lsam kill <app>
```

## Opérations de gestion

- Activer/Désactiver application au démarrage :
```n
lsam autostart on/off <app>
```

- Activer/Désactiver les privilèges d'une application :
```n
lsam root on/off <app>
```

- Renommer une application :
```n
lsam rename <app> <nouveau-nom>
```

- Changer le fichier de démarrage d'une application :
```n
lsam mainfile <app> <fichier>
```

## Supprimer une application

Il suffit d'exécuter la commande suivante et de confirmer avec 'y'
```n
lsam delete <app>
```

## Gestion des sauvegardes

**Remarque :** Les sauvegardes sont stockées dans le dossier `/home/lsam/backups`

- Sauvegarder une application :
```n
lsam backup <app>
```

- Sauvegarder toutes les applications :
```n
lsam backup-all
```

- Lister toutes les sauvegardes du serveur :
```n
lsam list-backups
```

- Lister toutes les sauvegardes d'une application :
```n
lsam list-backups <app>
```

- Supprimer une sauvegarde :
```n
lsam delete-backup <sauvegarde>
```

- Restaurer une sauvegarde :
```n
lsam restore-backup <sauvegarde>
```

## Importation/Exportation d'une application

- Exporter une application :
```n
lsam export <application>
```

- Importer une application depuis un .tar.gz :
```n
lsam import <archive>
```