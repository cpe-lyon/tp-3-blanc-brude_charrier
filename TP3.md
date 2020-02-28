# CR ADMIN SYSTEME TP3 
### Julien BLANC-BRUDE
### Lucie CHARRIER
### 28 février 2020

## Exercice 1
### 1. Quels sont les 5 derniers paquets installés sur votre machine?
_grep installed /var/log/dpkg.log | tail -5_ <br>
Cette commande permet d'afficher les 5 dernières lignes du fichier dpkg.log contenant le mot installed. On relève donc les 5 derniers paquets installés.
<br>
### 2. Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel!). Comment explique-t-on la (petite) différence de comptage ?
En utilisant la commande _dpkg -l |wc -l_ , on compte le nombre de lignes contenue dans le fichier dpkg.log. On en récupère 553.<br>
La commande _apt list |grep installé |wc -l_ nous retourne 548 lignes comptées.<br>
On explique cette différence ///////////////////////////////
<br>
### 3. Combien de paquets sont disponibles en téléchargement ?
_apt list |wc -l_ <br>
Nous retourne 61599, c'est le nombre que paquets installés et instalables.<br>
Pour avoir le nombre de paquets disponibles en téléchargement, on fait donc 61599 - 548 = 61051 paquets.
### 4. Créer un alias “maj” qui met à jour le système.
_alias maj='sudo apt update && sudo apt upgrade'_ 
<br>
### 5. A quoi sert le paquet fortunes? Installez-le.
Le paquet fortunes permet d'afficher des citations, proverbes, adages ... à chaque connexion en mode terminal.<br>
_sudo apt install fortunes_
<br>
### 6. Quels paquets proposent de jouer au sudoku ?
Le paquet sudoku (oui oui)<br>
_sudo apt install sudoku_
<br>
### 7. Lister les derniers paquets installés explicitement avec la commande apt install.
_grep "apt install" /var/log/apt/history/log_ <br>
Affiche : <br>
apt install fortunes <br>
apt install sudoku <br>
Soit les deux paquets installés avec apt install depuis l'installation de la VM.

## Exercice 2
