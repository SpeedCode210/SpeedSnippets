# Commandes de base APT

APT est l'outil de gestion des paquets dans Debian et dérivées (Ubuntu, Mint, PopOS...etc).

**NB :** Toutes les commandes doivent être exécutées en tant que `root`.


## Mise à jour la liste des paquets disponibles
Cette commande devrait être exécutée avant chaque installation ou mise à jour
```
apt update
```
 
## Installation / Désinstallation
- Installation :
```
apt install <nom-paquet>
```
- Désinstallation :
```
apt remove <nom-paquet>
```
- Désinstallation avec dépendances inutilisées :
```
apt autoremove <nom-paquet>
```
- Désinstallation et suppression de la configuration :
```
apt purge <nom-paquet>
```

## Mise à jour
- Mise à jour des paquets :
```
apt upgrade
```

## Réinstallation d'un paquet
```
apt install <nom-paquet> --reinstall
```

## Recherche d'un paquet
```
apt search <recherche>
```

## Listage des paquets
- Lister tous les paquets disponibles dans les dépôts :
```
apt list
```
- Lister tous les paquets installés sur la machine :
```
apt list --installed
```

## Affichage des informations d'un paquet
```
apt show <nom-paquet>
```
