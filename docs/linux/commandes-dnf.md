# Commandes de base DNF

DNF est l'outil de gestion des paquets dans Fedora et dérivées depuis Fedora 22 et RHEL 8 (et dérivées).

**NB :** Toutes les commandes doivent être exécutées en tant que `root`.

## Installation / Désinstallation
- Installation :
```
dnf install <nom-paquet>
```
- Désinstallation :
```
dnf remove <nom-paquet>
```
- Désinstallation avec dépendances inutilisées :
```
dnf autoremove <nom-paquet>
```

## Mise à jour
- Mise à jour d'un paquet :
```
dnf upgrade <nom-paquet>
```
- Mise à jour de la distribution :
```
dnf upgrade
```
- Mise à jour de la distribution en excluant un paquet (vous pouvez en mettre plusieurs séparés par des virgules) :
```
dnf upgrade --exclude=<nom-paquet>
```

## Rétrograder la version d'un paquet

```
dnf downgrade <nom-paquet>
```

## Réinstallation d'un paquet
```
dnf reinstall <nom-paquet>
```

## Recherche d'un paquet
```
dnf search <recherche>
```

## Listage des paquets
- Lister tous les paquets disponibles dans les dépôts :
```
dnf list
```
- Lister tous les paquets installés sur la machine :
```
dnf list installed
```

## Affichage des informations d'un paquet
```
dnf info <nom-paquet>
```

## Afficher l'historique des transactions
Affiche l'historique de toutes les commandes dnf exécutées depuis l'installation du système
```
dnf history
```

## Modules DNF

- Lister les modules :
```
dnf module list
```

- Lister les versions d'un module en particulier :
```
dnf module list <module>
```

**Exemple pour nodejs :**
```
dnf module list nodejs
```
```
Fedora Modular 36 - x86_64
Name       Stream     Profiles                             Summary              
nodejs     14         common [d], development, minimal     Javascript runtime   
nodejs     16         common [d], development, minimal     Javascript runtime   

Fedora Modular 36 - x86_64 - Updates
Name       Stream     Profiles                             Summary              
nodejs     14         common [d], development, minimal     Javascript runtime   
nodejs     16         common [d], development, minimal     Javascript runtime   
nodejs     18         common, development, minimal         Javascript runtime   

Hint: [d]efault, [e]nabled, [x]disabled, [i]nstalled
```

- Activation d'un module (ou changement de version):
```
dnf module disable nodejs
dnf module enable nodejs:16
```

- Installation à la volée d'une version d'un module:
```
dnf module install nodejs:16
```