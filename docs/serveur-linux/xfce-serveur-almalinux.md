# Installer XFCE sur un serveur Almalinux

Dans ce tutoriel, nous allons voir comment installer XFCE sur Almalinux (et dérivées de RHEL) et le serveur RDP pour y accéder à distance.

## Installation du repo EPEL

```
dnf install epel-release
```

## Installation de XFCE

```
dnf groupinstall Xfce
dnf install google-noto-{mono-fonts,sans-fonts,serif-fonts} xdg-user-dirs
```

## Installation de XRDP

```
dnf install xrdp xrdp-selinux xorgxrdp
echo "startxfce4" > ~/.Xclients
chmod +x ~/.Xclients
systemctl enable --now xrdp
```

## Ajout des règles de Pare-feu

```
firewall-cmd --permanent --add-port=3389/tcp
firewall-cmd --reload
```

## Redémarrage du serveur
```
systemctl reboot
```

## Connexion à distance

Et voilà, maintenant il ne vous reste qu'à vous connecter à votre serveur avec votre client RDP préféré !