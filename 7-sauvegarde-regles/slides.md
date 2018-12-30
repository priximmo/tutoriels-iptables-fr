%title: iptables
%author: xavki

-> Sauvegarde de vos règles ? <-
========

* les règles sont souvent complexes à mettre en place

* en cas de perte cela peut être difficile à refaire

<br>
* sauvegarde

```
iptables-save > /etc/sav-iptables.rules
```


<br>
* restauration

```
iptables-restore < /etc/sav-iptables.rules
```

----------------------------------------------------------

->  Charger au plus tôt les règles <-


* redémarrage = phase de montage

* idée : charger les règles dès la première connexion réseau (eth0)

<br>
```
pre-up iptables-restore < /etc/sav-iptables.rules
```

donc dans conf eth0 :

```
auto eth0
iface eth0 inet static
...
	pre-up iptables-restore < /etc/sav-iptables.rules 
```

