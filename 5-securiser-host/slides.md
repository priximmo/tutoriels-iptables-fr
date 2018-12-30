%title: iptables
%author: xavki

-> Sécuriser une machine avec iptable <-
========

<br>
* sécurisation réseau (les principes)
	- ce ne sont que des principes
	- on refuse tout (entrants/sortants)
	- on autorise au fur et à mesure des besoins

* si nécessaires : supprimer les règles

```
iptables -t filter -F
```

Rq : filter = toutes les tables

-------------------------------------------------------

-> Redéfinition des tables <-



* Refuser toutes les connexions par défaut:

```
iptables -t filter -P INPUT DROP
iptables -t filter -P FORWARD DROP
iptables -t filter -P OUTPUT DROP
```
Rq : -P = par défaut

* Si la machine établie une connexion on laisse passer la communication

```
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
```

Rq : -A = ajout de la règle à la fin (les règles sont prises dans l'ordre)

------------------------------------------------------


-> Redéfinition des tables <-


* on accepte les pings

```
iptables -t filter -A INPUT -p icmp -j ACCEPT
iptables -t filter -A OUTPUT -p icmp -j ACCEPT
```

* Option : ssh sur le 2222 (conf ssh) et on autorise celui-ci (attention)

```
iptables -t filter -A INPUT -p tcp --dport 2222 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 2222 -j ACCEPT
```

--------------------------------------------------------


-> Et bien d'autres règles <-

* suivant le type de machine (type serveur/machine perso)

* Pourront s'ajouter :
	- port 80 : http
	- port 443 : https
	- port 25 : smtp
	- port 587 : smtps
	- port 53 : dns
	- port 20 : ftp
	- port 990 : ftps
	- port 110 : pop3
	- port 995 : pop3s
	- port 143 : imap 



