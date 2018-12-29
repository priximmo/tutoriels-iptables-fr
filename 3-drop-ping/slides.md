%title: iptables
%author: xavki

-> Mise en pratique <-
========

* Empêcher les pings en entrée

	- ping = protocole icmp

```
iptables -I INPUT -p icmp --icmp-type 8 -j DROP

iptables -L
```

Rq :
type 8 =  "Echo Request" pour le ping réseau 
-I : ajoute les règles au début de la table

	- suppression des règles

```
iptables -F
```

--------------------------------------------------------

* Empêcher les pings en sortie

```
iptables -I OUTPUT -p icmp -j DROP

iptables -L
```

* Supprimer une règle précise

```
iptables -L --line-numbers

iptables -D OUPUT "num_ligne"
```

