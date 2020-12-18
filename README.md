# Cours d'initiation à Kubernetes

## Prérequis

Afin de pouvoir réaliser des TPs à distance, vous devez impérativement
avoir un ordinateur sur lesquels sont installés *Virtual Box* et *Vagrant*.
Nous allons donc commencer par voir comment les installer.

### Installation de Virtual Box

```
sudo apt install virtualbox
```

### Installation de Vagrant

Téléchargez la dernière version de Vagrant sur leur <a href="https://www.vagrantup.com/downloads">site web</a>.

Puis, dans le répertoire où vous avez téléchargé le fichier `.deb`
```
sudo dpkg -i vagrant_2.2.13_x86_64.deb
```
(Modifiez le nom du fichier si la version n'est plus la même).

Testez que votre installation a fonctionné
```
vagrant version
```

### Création de votre espace de travail.

Clonez le dossier gitlab du cours.

```
git clone git@gitlab.mipn.fr:julien.david/k8s.git
```

### En cas de problème

Contactez moi avant la première séance, qui aura lieu le mardi 23 Novembre, 
sur Mattermost.