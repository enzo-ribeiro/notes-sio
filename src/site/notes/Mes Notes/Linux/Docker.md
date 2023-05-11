---
{"dg-publish":true,"permalink":"/mes-notes/linux/docker/"}
---

Contrairement à une virtualisation un container docker partage les mêmes composants que le système déjà présent sur la machine que nous utilisons. Il virtualisera les applications et non le système.

Pour commencer à utiliser docker il faut l'installer avec la commande suivante :
```Shell
sudo -s
apt install docker.io docker-compose git -y
```
Une fois installer on peut se rendre sur le site `< https://hub.docker.com >` pour y choisir les containers qu enous voulons. Ici nous choisirons ubuntu.
```Shell
docker pull ubuntu:latest
```
où `<latest>` correspond à la version la plus récente (Si vous cherchez une version spécifique il faudra changer la version). Le `<pull>` sert à installer le container. Pour voir les containers installé il faut taper le commande suivante :
```Shell
docker images
### resultat :
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              3b418d7b466a        2 weeks ago         77.8MB
```
Pour démarrer ce container il faut renseigner la commande suivante :
```Shell
docker run -it --name ubuntu_test ubuntu 
```
- `<-it>` sert à rendre le container "intéractif".
- `<--name>` sert à donner un nom, cette commande est suivie du nom ici "ubuntu_test".
- `<ubuntu>` est pour déclarer l'image que nous souhaitons démarrer. 
```Shell
root@2b0ec31dd39e:/$ cat /etc/lsb-release
### résultat :
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=22.04
DISTRIB_CODENAME=jammy
DISTRIB_DESCRIPTION="Ubuntu 22.04.2 LTS"
```
Nous pouvous voir que nous sommes bien sur notre container qui est bien une Ubuntu 22.04.2.
Pour quitter le container on puet simplement rentrer la commande `<exit>` ou le mettre en arrière plan sans arréter le container `<Ctrl> + <P> & <Ctrl> + <Q>`
Avec la commande suivante on peut voir :
```Shell
docker ps -a
### résultat : 
CONTAINER ID    IMAGE   COMMAND      CREATED          STATUS            NAMES
2b0ec31dd39e   ubuntu  "/bin/bash"  10 minutes ago    Up 10 minutes   ubuntu_test
```
- `<CONTAINER ID>` l'identifiant de container
- `<IMAGE>` l'image utilisé pour le container
- `<COMMAND>` la commande lancé de base "bin/bash" pour lancer le terminal
- `<CREATED>` quand à-t-elle été créée
- `<STATUS>` montre le status du container (varie selon la façon utilisé pour quitter le container)
- `<NAMES>` affiche le nom que nous avons donné plus haut

Si le container à été mis en pause (avec la combinaison de touche) il est possible de renprendre la main dessus sans avoir à relancer le container : 
```Shell
docker attach ubuntu_test
```
Il est également possible d'exectuter des commandes alors que nous sommes pas atteché avec mle container visé:
```Shell
docker exec -it ubuntu_test whoami
### résultat :
root
```
- `<exec>` déclare que nous voulons executer une commande sur la machine
- `<ubuntu_test>` déclare le container où nous voulons executer la commande
- `<whoami>` commande que j'ai executé sur le container

Pour finir voici un petit résumé des commandes possible avec docker :
- `<docker pull>` télécahrge une image
- `<docker start>` démarre un container
- `<docker run>` rassemble la commande `<docker pull>` & `<docker start>` 
- `<docker stop>` arrète le container
- `<docker attach>` s'attache au container
- `<docker exec>` execute un commande dans le container sans se réattacher à celui ci
- `<docker rm>` supprime la machine déclaré 