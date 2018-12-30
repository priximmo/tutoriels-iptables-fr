%title: iptables
%author: xavki

-> Mise en pratique <-
========

<br>
* Empêcher les pings en entrée

```
  +------------+        +------------+
  | 172.17.0.1 +--------> 172.17.0.2 |
  +------------+        +------------+  
                        x 
                        |
```
- ping = protocole icmp
- on travaille sur 172.17.0.2

<br>
```
iptables -I INPUT -p icmp --icmp-type 8 -j DROP
iptables -L
```

Rq :
type 8 =  "Echo Request" pour le ping réseau 
-I : ajoute les règles au début de la table

<br>
	- suppression des règles

```
iptables -F
```

--------------------------------------------------------

* Empêcher les pings en sortie

```
  +------------+        +------------+
  | 172.17.0.1 +--------> 172.17.0.2 |
  +------------+        +------------+  
               x 
               |
```

- on travaille sur 172.17.0.1

```
iptables -I OUTPUT -p icmp -j DROP

iptables -L
```

* Supprimer une règle précise

```
iptables -L --line-numbers

iptables -D OUPUT "num_ligne"
```

