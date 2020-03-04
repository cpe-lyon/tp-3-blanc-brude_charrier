# CR ADMIN SYSTEME TP3 
### Julien BLANC-BRUDE
### Lucie CHARRIER
### 28 février 2020

## Exercice 1
### 1. Quels sont les 5 derniers paquets installés sur votre machine?
`grep installed /var/log/dpkg.log | tail -5` <br>
Cette commande permet d'afficher les 5 dernières lignes du fichier dpkg.log contenant le mot installed. On relève donc les 5 derniers paquets installés.
<br>
### 2. Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel!). Comment explique-t-on la (petite) différence de comptage ?
En utilisant la commande `dpkg -l |wc -l` , on compte le nombre de lignes contenue dans le fichier dpkg.log. On en récupère 553.<br>
La commande `apt list |grep installé |wc -l` nous retourne 548 lignes comptées.<br>
On explique cette différence car les packets qui permettent de gérer apt sont compris dans la liste des dpkg.
<br>
### 3. Combien de paquets sont disponibles en téléchargement ?
`apt list |wc -l` <br>
Nous retourne 61599, c'est le nombre que paquets installés et instalables.<br>
Pour avoir le nombre de paquets disponibles en téléchargement, on fait donc 61599 - 548 = 61051 paquets.
### 4. Créer un alias “maj” qui met à jour le système.
`alias maj='sudo apt update && sudo apt upgrade'` 
<br>
### 5. A quoi sert le paquet fortunes? Installez-le.
Le paquet fortunes permet d'afficher des citations, proverbes, adages ... à chaque connexion en mode terminal.<br>
`sudo apt install fortunes`
<br>
### 6. Quels paquets proposent de jouer au sudoku ?
Le paquet sudoku (oui oui)<br>
`sudo apt install sudoku`
<br>
### 7. Lister les derniers paquets installés explicitement avec la commande apt install.
`grep "apt install" /var/log/apt/history/log` <br>
Affiche : <br>
_apt install fortunes_ <br>
_apt install sudoku_ <br>
Soit les deux paquets installés avec apt install depuis l'installation de la VM.

## Exercice 2
`dpkg -S $(which ls)`<br>
ls est contenu dans le paquet _coreutils : /bin/ls_ <br>

Le script bash est le suivant : <br>
`#!/bin/bash` <br>
`dpkg -S(which $1)`<br>

De cette façon, l'utilisateur passe une commande en paramètre et le paquet qui l'a installé est retourné.

## Exercice 3
`#!/bin/bash`<br>
`if [[ $(dpkg -l |awk '{print $2}') =~ $1]]; then`<br>
`   echo "INSTALLE"`<br>
`else`<br>
`   echo "NON INSTALLE`<br>
`fi`

## Exercice 4
`dpkg -L coreutils | more` <br>
La commande "[]" réalise un test, elle exécute l'instruction donnée dans les crochets et retourne le résultat ou une erreur.

## Exercice 5
Afin d'accéder à l'interface graphique, il faut d'abord installer aptitude puis le lancer.<br>
Un fois lancé, nous recherchons emacs (presser plusieurs fois n pour trouver Emancs et ses dépendances) puis presser "+" pour l'installer.

## Exercice 6
Les lignes de commandes indiquées retournent l'erreur suivante : le paquet oracle-java11-installer est obselète ou manquant mais peut être remplacé par le paquet suivant "oracle-java11-installer-local".<br>
Nous décidons d'accepter d'installer ce paquet.<br>
`cd /etc/pat/sources/list.d` <br>
`ls`<br>
Nous retourne : _linuxuprising-ubuntu-java-eoan.list_ <br>
Le fichier a donc bien été crée, il contient les dépots demandés à l'installation tel que _`deb http://ppa.launchpad.net/linuxuprising/java/ubuntu eoan main`_

## Exercice 7
__Création d'un paquet Debian avec dpkg-deb__ <br>
On déplace origine commande à user/local/bin avec la commande `mv origine-commande user/local/bin`<br>
On crée ensuite un fichier control avec les informations demandées. Pour écrire dedans, nous demandons l'écriture jusqu'a ce qu'on redonne la clé "FIN"<br>
`cat <<FIN>> control`<br>
On construit ensuite le paquet avec la commande indiquée.<br>

__Création du dépot personnel avec reprepro__ <br>
De même que precedemment, nous créons le fichier distributions dans repo-cpe/conf avec la commande `cat <<FIN>> distributions`.<br>
Il faut également installer le paquet reprepro `sudo apt install reprepro`.<br>

`reprepro -b . includedeb cosmic origine-commande.deb`<br>
// Ne fonctionne pas.<br>
__Signature du dépot avec CPG__<br>



## Exercice 8


