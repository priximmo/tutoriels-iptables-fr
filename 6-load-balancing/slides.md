%title: iptables
%author: xavki

-> ipTables comme load-balancer ?!?! <-
========

* couche base : osi 4 (transport)

```
                                      +-----------+
                                    +-> 172.17.0.3|
 +-------------+    +-------------+ | +-----------+
 |  172.17.0.1 +-----> 172.17.0.2 +-+
 +-------------+    +-------------+ | +-----------+
    client             router       +-> 172.17.0.4|
                                      +-----------+
```

---------------------------------------------------------

-> Au taff !!! <-

* Requête de départ à acheminer sur 172.17.0 3-4

```
echo "toto" | nc 172.17.0.2 5000

```

* Configuration du router

Pour gérer les paquets à l'aller:

```
iptables -A PREROUTING -t nat -p tcp -d 172.17.0.2 --dport 5000 -j DNAT --to-destination 172.17.0.3:5000
```

Pour prévoir le retour:

```
iptables -A POSTROUTING -t nat -p tcp -d 172.17.0.3 --dport 5000 -j SNAT --to-source 172.17.0.2
```

---------------------------------------------------------

-> Et le load-balancing ??? <-



Pour simplifier on choisir le Round Robin (chacun son tour) :


	- un paquet sur deux on skip

```
iptables -A PREROUTING -t nat -p tcp -d 172.17.0.2 -m statistic --mode nth --every 2 --packet 0 --dport 5000 -j DNAT --to-destination 172.17.0.3:5000
```


	- l'autre route récupère les paquets restants

```
iptables -A PREROUTING -t nat -p tcp -d 172.17.0.2 --dport 5000 -j DNAT --to-destination 172.17.0.4:5000
```


