# Commandes de base Pacman

Pacman est le gestionnaire de paquets de Archlinux et ses dérivées, il permet de gérer facilement les paquets depuis les dépôts officiels ou des paquets de l'utilisateur.

**NB :** Toutes les commandes doivent être exécutées en tant que `root`.

## Actualisation de la liste en cache des dépôts

```
pacman -Sy
```

## Installation / Désinstallation
- Installation :
```
pacman -S <nom-paquet>
```
- Désinstallation :
```
pacman -R <nom-paquet>
```
- Désinstallation avec dépendances inutilisées :
```
pacman -Rs <nom-paquet>
```

## Mise à jour
- Mise à jour des paquets :
```
pacman -Syu
```

## Réinstallation d'un paquet
```
pacman -S <nom-paquet>
```

## Recherche d'un paquet
```
pacman -Ss <recherche>
```

## Listage des paquets
- Lister tous les paquets disponibles dans les dépôts :
```
apt list
```
- Lister tous les paquets installés sur la machine :
```
pacman -Q
```
- Savoir si un paquet est installé :
```
pacman -Q <nom-paquet>
```

## Affichage des informations d'un paquet
```
pacman -Si <nom-paquet>
```
