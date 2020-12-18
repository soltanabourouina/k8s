# Premiers conteneurs
## Namespaces

Lister la liste des namespaces sur votre machine.

## Unshare

Pour cet exercice, la lecture de la **manpage** de la commange `unshare` est fortement conseillée. 
De plus, si votre terminal le permet, il est conseillé de découper/splitter celui-ci en deux,
afin de pouvoir d'un côté regarder les résultats d'une commande dans un conteneur et de l'autre
les résultats de la même commande hors du conteneur.

### Espaces de nommage réseau et PID.

- Listez la liste de vos interfaces réseaux à l'aide de la commade 
`ip addr show`
- Listez la liste des processus avec `ps -aux`.
- Créez un conteneur avec des nouveaux espaces de nommage réseau et PID. 
- Réexécutez la commande `ip addr show`. Qu'observez-vous?
- Réexécutez la commande `ps -aux`. Qu'observez-vous?

### Espace de nommage utilisateur 

- Créez un conteneur qui possède les droits d'un utilisateur sans privilège à l'extérieur
du conteneur mais les droits root à l'intérieur.
- Créez un fichier `test.txt` à l'intérieur du conteneur.
- A l'intérieur du conteneur, qui est le propriétaire du fichier `test.txt`?
- Même question à l'extérieur du conteneur.


## CGroups

### Limitation des ressources

- Installez le package `cgroup-tools` à l'aide de la commande:
```sudo apt install cgroup-tools ```
- Créez un groupe de contrôle dans lequel la RAM est limitée à 2 Mo.
- Exécutez un `bash` avec ce groupe de contrôle.
- Tentez d'ouvrir un éditeur de texte dans ce conteneur. Que se passe t-il?
- Redémarrez l'ordinateur.
- Le groupe de contrôle existe t-il encore?


# Vagrant

## Installation

- Si ce n'est pas déjà fait, installez vagrant

```
sudo apt update
sudo apt install virtualbox vagrant
 ```

- Télécharger dans un même répertoire (celui où vous ferez le TP) les fichiers 
  - Vagrantfile
  - install_common.sh
  - install_master.sh
  - install_node.sh
- Dans ce même répertoire, créez les machines virtuelles en lançant la commande
`vagrant up` 
- Vérifiez que les deux machines virtuelles tournent en utilisant la commande
`vagrant status`

**Attention, cette commande prend du temps.**

## Configuration

- connectez vous au noeud master:
```
vagrant ssh kmaster
 ```
- Entrez les commmandes suivantes:

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
export kubever=$(kubectl version | base64 | tr -d '\n')
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"
 ```

Attendre que la commande `kubectl get nodes` affiche **Ready** pour les statuts (environ une minute).


## Installation de Kubernetes

- Lisez les fichiers de configuration `install_*.sh`.
- Quelles sont les commandes utilisées pour l'installation de Kubernetes?
Décrire à quoi servent chacune des commandes.

## Composants de kubernetes

Pour cet exercice, ouvrez en parallèle deux terminaux (ou scindez en un en deux).
Connectez vous à *kmaster* et à *knode1* (une connection par terminal).
Sur les deux serveurs, effectuez la commande:
```
sudo docker ps
 ```
Quels sont les conteneurs qui tournent sur ces machines ?
A quoi servent chacun de ces conteneurs?

## Réseau

Dessinez les réseaux désormais présent sur votre machine
- votre réseau local connecté à internet
- le réseau vagrant
- le réseau kubernetes