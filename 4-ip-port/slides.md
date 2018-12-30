%title: iptables
%author: xavki

-> Mise en pratique suite <-
========

<br>
* outils utiles pour faire des tests :

Mettre en place une socket écoutant sur le port 8000 :

```
python -m SimpleHTTPServer 8000
```

Lister les ports en écoute à distance :

```
nmap -PM ip_machine
```

Test ouverture :

```
telnet ip_machine port

netcat ip_machine port < fichier
```

------------------------------------------------------------


-> Travail sur les ip et ports <-


```

                   OK       serveur (8000)
                        +------------+
                +-------> 172.17.0.2 |
                |       +------------+
  +-------------+              ^
  | 172.17.0.1  |              |
  +-------------+              |
     client                KO  |
                        +------------+
                        | 172.17.0.3 |
                        +------------+
                            client
```

-------------------------------------------------------------------


-> Mise en pratique <-



* empêcher d'entrée pour une machine

```
iptables -I INPUT -p tcp -dport 8000 -j DROP
iptables -I INPUT -s 172.17.0.1 -p tcp -dport 8000 -J ACCEPT
```

* empêcher d'aller vers une ip et un port

```
iptables -I OUTPUT -d 172.17.0.2 -p tcp --dport 8000 -j DROP
```

* et on supprimer la règle

```
iptables -L --line-numbers

iptables -D OUTPUT num_ligne
```
