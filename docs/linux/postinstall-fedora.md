# Post-installation de Fedora Workstation

Fedora Linux étant la distribution que j'utilise au quotidien, il m'arrive souvent de devoir l'installer/réinstaller et je me retrouve avec plusieurs paquets inutiles/alourdissant le système et d'autres manquants, par conséquent je résume toutes mes actions post-installation dans cet article. 

## Désinstallation de paquets inutiles

```
sudo dnf remove virtualbox-guest-additions podman httpd openssh-server
```

## Désinstallation des applications GNOME "inutiles"

```
sudo dnf remove cheese totem rhythmbox gnome-boxes gnome-calendar gnome-calculator gnome-clocks gnome-connections gnome-contacts gnome-characters gnome-maps gnome-photos gnome-tour gnome-weather gnome-screenshot
```
**NB :** GNOME Screenshot n'est inutile que depuis GNOME 42 rajoutant de nouvelles options de capture d'écran.

## Désinstallation de GNOME Software et PackageKit

Etant donné la forte consommation en ressources du démon PackageKit et de GNOME Software et le fait que j'installe mes programmes depuis le temrinal, je préfère les retirer afin d'alléger le système

```
sudo systemctl disable --now packagekit
sudo dnf remove gnome-software PackageKit
# Nettoyage du cache de PackageKit
sudo rm -rf /var/cache/PackageKit
```

## Ajout des dépôts RPM Fusion

```
# RPM Fusion free
sudo dnf install --nogpgcheck https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
# RPM Fusion non-free
sudo dnf install --nogpgcheck https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
# Si l'on décide d'ajouter les infos dans GNOME Software
sudo dnf install rpmfusion-free-appstream-data rpmfusion-nonfree-appstream-data
```

## Activation du dépôt Flathub

```
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
sudo flatpak remote-modify flathub --enable
```