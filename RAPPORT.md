j'ai directement supprimer le déploiement du tp2

> -      kubectl delete deployment monnginx													//sûppression de nginx
>       
>        kubectl create deployment myapache --image=apache     								//création du déploiment myapache
>       
>        kubectl autoscale deployment.v1.apps/myapache --min=1 --max=3 --cpu-percent=80     // utilisation de autoscale entre 1 et 3 répliques
>       
>        kubectl get deployment                             								//affichage des ddéploiments
>       
>        kubectl create service nodeport myapache --tcp=8080:30006   						//création du service
>       
>        nano mondeploiment.yml                												//creation du fichier yaml pour le déploiment dans kmaster
>       
>        nano service.yml                  													//creation du fichier yaml pour le service dans kmaster
>        
>        
>        
>        
>        **partie volume:**
>        
>        
>        
>       
>       étant sur kmaster : exit
>       
>       je me suis mise sur knode1 avec : vagrant ssh knode1
>       
>       -création de dossier tp : mkdir /home/vagrant/tp
>       
>       dans tp: création de index.php avec: vim index.php
>       
>       code PHP permettant d'afficher l'IP du serveur: 
>         <?php$ip_server = $_SERVER[['SERVER_ADDR'] ?>


-*- ps: vous trouverez des 2 captures dans le dossier k8s-*-
>

​     