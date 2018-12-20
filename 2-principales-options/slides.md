%title: iptables
%author: xavki

-> Principales options <-
=========




* -L : liste les règles




-> Type d'actions chaines/règles  <-



Actions sur les chaines : INPUT / OUTPUT / FORWARD
en majuscules

* -A : ajout de règle à une chaine (-A INPUT)

* -D : suppression de règle (-R INPUT 1 - numéro de la règle dans la chaine INPUT )

* -R : remplace la règle

* -I : insertion d'une règle (sans chiffre au début de la chaine (ex: INPUT 1)

* -F : flush les règles pour une chaine (-F INPUT)

* -N : création de chaîne

* -X : drop de chaine

* -P : définition de la policy d'une chaine (par défaut - ex: -P INPUT DROP)

------------------------------------------------------------------------------------


-> Caractéristiques  <-



* -p : protocole (-p tcp)

* -s : la source (ip, réseau)

* -j : action à faire (DROP/ACCEPT)

* -d : la destination (ip, réseau)

* -i : interface d'entrée (eth0...)

* -o : interface de sortie

* --sport 80 : un port

* -m multiport --sport 80,443 : plsueirus ports

* -t : type (NAT...)





