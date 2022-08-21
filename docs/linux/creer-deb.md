# Comment créer un paquet DEB

DEB est le format de fichier des paquets logiciels de la distribution Debian GNU/Linux. Presque toutes les distributions basées sur Debian telles que Ubuntu et Linux Mint utilisent aussi ce format.

Dans ce tutoriel, nous allons voir comment créer un paquet DEB.

## Installation des outils nécessaires

### Sous Debian et dérivées
```
sudo apt-get install fakeroot
```

### Sous Fedora et dérivées
```
sudo dnf install dpkg fakeroot
```

## Mise en place de l'arborescence de construction

```
mkdir -p <package_name>/DEBIAN
mkdir -p <package_name>/usr/bin
```

## Copie des fichiers

Mettez les binaires de votre paquet dans le dossier `<package_name>/usr/bin` (ou autre si nécessaire, selon l'emplacement ou ils seront installés)

## Création du fichier control

``<package_name>/DEBIAN/control``
```
Package: <package_name>
Version: 1.0
Maintainer: SpeedCode
Architecture: all
Description: package description 
```
Pour plus d'options sur le fichier control : [http://www.debian.org/doc/debian-policy/ch-controlfields.html#s-binarycontrolfiles](http://www.debian.org/doc/debian-policy/ch-controlfields.html#s-binarycontrolfiles) 

## Ajout d'un script post-installation (Facultatif)

``<package_name>/DEBIAN/postinst`` (Assurez-vous qu'il est exécutable)
```
#!/usr/bin/bash
# Mettez vos commandes à exécuter
```

## Construction du paquet

```
cd <package_name>/..
dpkg-deb --build <package_name>
```

La commande va créer le fichier <package_name>.deb, pour l'installer, il suffit d'exécuter la commande suivante :

```
dpkg -i <package_name>.deb
```