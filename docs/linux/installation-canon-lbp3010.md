# Installation de l'imprimante Canon LBP3010 sous Linux

## Téléchargement du pilote

Installez les RPM ou DEB (Selon la distribution et l'architecture) des paquets `cndrvcups-common` et `cndrvcups-capt` depuis le tar.gz téléchargeable à l'adresse suivante : [https://sg.canon/en/support/0100459601](https://sg.canon/en/support/0100459601)

## Redémarrage de CUPS

Pour que l'installation du pilote soit prise en compte par CUPS, executez la commande suivante :
```
sudo systemctl restart cups
```

## Sélection du PPD correspendant à l'imprimante

Vous pouvez voir la liste des fichiers PPD via la commande suivante :

```
ls /usr/share/cups/model/ | grep CNCUPS
```

Dans le cas de la LBP3010, il s'agit de `CNCUPSLBP3050CAPTK.ppd`

## Installation de l'imprimante

Branchez votre imprimante en USB, puis exécutez les commandes suivantes :
**NOTE :** Remplacez `/dev/usb/lp0` par l'emplacement du fichier du périphérique si nécessaire, vous pouvez voir la liste des périphériques via la commande `ls -l /dev/usb`

```
sudo /usr/sbin/lpadmin -p LBP3010 -m CNCUPSLBP3050CAPTK.ppd -v ccp://localhost:59787 -E
sudo /usr/sbin/ccpdadmin -p LBP3010 -o /dev/usb/lp0
sudo service ccpd restart
```

Vous pouvez voir le statut su démon ccpd via la commmande suivante : 
```
sudo service ccpd status
# Exemple : 
# /usr/sbin/ccpd: 81161 81151
```

Et pour vérifier l'installation de l'imprimante :
```
sudo ccpdadmin
```

Et pour vérifier l'état de l'imprimante :
```
captstatusui -P LBP3010
```

## Démarrage automatique du démon ccpd

Ajoutez simplement la ligne suivante à cron (commande : `export VISUAL=nano;sudo -E crontab -e`)

```
@reboot service ccpd start
```