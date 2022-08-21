# Comment créer un paquet RPM

RPM (Red Hat Package Manager), est un système de gestion de paquets de logiciels utilisé sur certaines distributions GNU/Linux. C'est le format utilisé par Linux Standard Base (LSB), il est utilisé par plusieurs distributions : Fedora Linux, RHEL, CentOS, OpenSUSE...etc

Dans ce tutoriel, nous allons voir comment créer un paquet RPM sous Fedora et CentOS.

## Installation des outils nécessaires

```
sudo dnf install dnf-utils rpmdevtools rpmlint
```

## Mise en place de l'arborescence de construction

Afin de construire notre paquet, nous devrons tout d'abord mettre en place uen hiérarchie spécifique via la commande suivante :

```
rpmdev-setuptree
```

Un dossier `rpmbuild` sera créé dans votre dossier `home` avec la structure suivante :
```
rpmbuild 
 |- BUILD 
 |- RPMS 
 |- SOURCES 
 |- SPECS 
 |- SRPMS 
```

- Le dossier BUILD est utilisé lors de la construction du RPM, les fichiers tomporaires sont placés dedans.
- Le dossier RPMS contient les paquets générés.
- Le dossier SOURCES sert à contenir les sources (script, project complexe, ou programme précompilé), souvent compressées dans des archives .tar.gz ou .tgz.
- Le dossier SPEC contient les fichiers .spec. Le fichier .spec définit comment un paquet est construit.
- Le dossier SRPMS contient les paquets .src.rpm. Ils ne sont pas affiliés à une architecture ou une distribution. Les rpm sont construits à partir de ces fichiers.

## Préparation de l'archive des sources

Dans cet exemple, nous allons le faire pour un programme `test-app` en version `1.0`, créez le dossier `test-app-1.0` puis mettez-y les binaires de votre applications et créez l'archive depuis le dossier parent avec la commande suivante :

```
tar -czvf test-app-1.0.tar.gz test-app-1.0
```

Déplacez ensuite l'archive vers le dossier SOURCES

```
mv test-app-1.0.tar.gz ~/rpmbuild/SOURCES/
```

## Création du fichier .spec

Executez la commande suivante :

```
cd ~/rpmbuild/SPECS
rpmdev-newspec test-app
```

Mettez-y ce contenu à peu près :

```
Name:           test-app
Version:        1.0
Release:        1%{?dist}
Summary:        A test app

License:        
URL:            
Source0:        %{name}-%{version}.tar.gz

%description
A test app

%prep
%setup -q

%install
# Remplissez ici


%files
# Remplissez ici



%changelog
* Wed Aug 17 2022 Raouf Ould Ali <raouf@eclipium.xyz>
- First Version
```

### Exemple concret sur TetraSwap

```
%global __provides_exclude_from /*
%global __requires_exclude_from /*
Name:           tetraswap
Version:        1.3.2
Release:        1%{?dist}
Summary:        A simple but challengeous puzzle game !

License:        Proprietary
URL:            https://eclipium.xyz/tetraswap
Source0:        %{name}-%{version}.tar.gz

%description
A simple but challengeous puzzle game !

%prep
%setup -q

%install
rm -rf $RPM_BUILD_ROOT
mkdir -p $RPM_BUILD_ROOT/%{_bindir}/TetraSwap
mkdir -p $RPM_BUILD_ROOT/usr/share/applications
cp -r ./* $RPM_BUILD_ROOT/%{_bindir}/TetraSwap
mv $RPM_BUILD_ROOT/%{_bindir}/TetraSwap/TetraSwap.desktop $RPM_BUILD_ROOT/usr/share/applications/TetraSwap.desktop

%files
/usr/bin/TetraSwap/*
/usr/share/applications/TetraSwap.desktop
``` 

Remplissez selon les besoins de votre paquet, puis passez à l'étape suivante.
Si vous vous y perdez un peu, vous pouvez vous aider de cet article : [https://wiki.cdot.senecacollege.ca/wiki/RPM_spec_File_Contents](https://wiki.cdot.senecacollege.ca/wiki/RPM_spec_File_Contents)

Une fois la configuration terminée, vous pouvez vérifier votre fichier .spec via la commande suivante :

```
rpmlint ~/rpmbuild/SPECS/test-app.spec
```

## Construction du paquet

Nous allons construire le .src.rpm et le .rpm via la commande suivante :
```
rpmbuild -ba ~/rpmbuild/SPECS/test-app.spec
```
Ou sinon le .src.rpm seulement :
```
rpmbuild -bs ~/rpmbuild/SPECS/test-app.spec
```
Puis le .rpm via la commande suivante :
```
rpmbuild -bb ~/rpmbuild/SPECS/test-app.spec
```

Et voilà, nous venons de contruire notre paquet RPM !
