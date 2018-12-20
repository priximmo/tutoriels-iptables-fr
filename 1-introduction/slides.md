%title: iptables
%author: xavki

-> IPTABLES : intérêt <-
=========

* firewall : parefeu = sécurité
	- filtrage ip
	- filtre ports
	- filtrage protocole
	- translations (changement ip etc...)
	- modifications de paquets

* on parle aussi de netfilter

* installation :

```
sudo apt-get install iptables
```

-----------------------------------------------------------------------------

-> Tables <-

* la table NAT :
	- translation de ports et d'ip
	- deux localisations :
		- PREROUTING : amont parefeu
		- POSTROUTING : aval du parefeu
	- 3 targets :
		- DNAT : IP de destination
		- SNAT : IP source
		- MASQUERADE : simule une gateway

* la table filter :
	- 3 chaines :
		- INPUT : les entrants
		- OUPUT : les sortants
		- FORWARD : les passants
	- 4 targets :
		- DROP : refus brut des paquets sans retour
		- ACCEPT : accepte les paquets 
		- REJECT : rejet avec retour à l'expéditeur
		- DENY
		... LOG : logger les paquets sur la sortie standard

* la table mangle : modification des paquets
	- 5 targets :
		- TOS : type de service (type of service)
		- TTL : durée de vie (time to live)
		- MARK : marquer les paquets (taggage)
		- SECMARK : marquage de sécurité (pour outils de sécurité type SE Linux)
		- CONNSECMARK : copie d'un cas de sécurité


