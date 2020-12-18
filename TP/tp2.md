Dans l'intégralité du TP, les exercices se feront sur le serveur virtuel **kmaster**
que nous avons configuré la semaine dernière.
Commencez par relancer vagrant. Placez vous dans le répertoire contenant le
fichier Vagrantfile est entrez la commande:
```vagrant up```
Une fois les serveurs lancés, faites un:
```vagrant ssh kmaster```

Si vous souhaitez copier un fichier sur les machines virtuelles, utilisez la 
commande suivante:
```scp -P 2222 nom_du_fichier vagrant@127.0.0.1:.```
Mot de passe: `vagrant`


# Préparation au TP noté

Demain, vous devrez rendre votre TP via gitlab, pour cela, je veux m'assurer que vous savez tous
pousser une nouvelle branche.
- dans un terminal, dans le répertoire `k8s`, tapez la commande
  ```git checkout -b NOM_PRENOM```
- pour ajouter un fichier au rendu, tapez `git add nom_du_fichier`
- pour envoyer une version de votre tp, tapez
```
git commit -am "un commentaire"
git push
 ```


# Déploiement d'un serveur nginx

- Créez un déploiement d'un serveur **nginx**, contenant deux pods identiques. 
- Listez les ressources qui tournent sur le cluster (pods, déploiements, services, replicaSet)
- Que remarquez vous concernant le nom du ReplicaSet et des pods?
- Créez un service permettant d'obtenir l'accès au serveur nginx.
- Testez que cela fonctionne sur votre navigateur.
- Supprimez le déploiement.


## Création de secrets

Nous allons commencer par en créer un:
```
echo -n "incroyable-mdp-du-tp-sur-k8s" | base64
 ```
Vous devriez voir le résultat suivant:
`aW5jcm95YWJsZS1tZHAtZHUtdHAtc3VyLWs4cw==`

Sur le serveur kmaster, créez un fichier `secret.yml` contenant ceci: 
```
---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secrets
type: Opaque
data:
  ROOT_PASSWORD: aW5jcm95YWJsZS1tZHAtZHUtdHAtc3VyLWs4cw==
 ```

**ATTENTION: L'INDENTATION EST ESSENTIELLE EN YAML**

Puis ajoutez ce secret à Kubernetes:
```
kubectl apply -f secret.yml
 ```
Vérifiez que le secret a bien été ajouté. Pour cela, affichez la liste des secrets
et demandez la description du secret nommé **mysql-secrets**
<!-- kubectl get secret -->

## Dévoiler le secret

- Créez un fichier `deploiement_secret.yml` dans lequel vous décrirez le même déploiement qu'au premier exercice (nginx avec deux pods)
- Ajoutez le secret `mysql-secrets` dans votre déploiement et donnez la possibilité d'accéder au secret depuis le fichier `/usr/share/nginx/html/secret.txt`

Vous vous aiderez de cette page:
https://kubernetes.io/fr/docs/concepts/configuration/secret/

- Sur le noeud `knode1`, tapez la commande `sudo docker ps`
- Choissez un des deux conteneurs nginx (copiez le CONTAINER_ID) et tapez la commande
```docker exec -ti CONTAINER_ID /bin/bash ```
- Une fois dans le conteneur, dans le répertoire `/usr/share/nginx/html/`,
  décodez le secret et créez un fichier `index.html` contenant le secret décodé.
- Créez un service permettant d'obtenir l'accès aux serveurs `nginx` et vérifiez dans un navigateur que ce qui s'affiche n'est pas toujours la même chose (Parfois le secret, parfois non).

## Envoyez votre TP sur gitlab

(voir début du sujet de TP)

- Ajoutez votre fichier `deploiement_secret.yml` sur votre branche.