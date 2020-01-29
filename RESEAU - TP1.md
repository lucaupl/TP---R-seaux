# RESEAU - TP1             
**THOMAS FORD, RICHARD LUCAS, TEXIER MARC, DAVID BORIS**

## PARTIE 1

### Exploration locale en solo
Device: Macbook Pro
iOS: 10.15.1

lucasrichard@MacBook-Pro-de-Lucas ~ % **ifconfig**

#### LOOPBACK

lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	options=1203<RXCSUM,TXCSUM,TXSTATUS,SW_TIMESTAMP>
	inet 127.0.0.1 netmask 0xff000000 
	inet6 ::1 prefixlen 128 
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1 
	nd6 options=201<PERFORMNUD,DAD>
    
#### WIFI 

en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	options=400<CHANNEL_IO>
	ether a4:83:e7:76:3c:5e 
	MAC -> **inet6 fe80::845:f25:889c** 9053%en0 prefixlen 64 secured scopeid 0x6 
	**inet 10.33.1.147** netmask 0xfffffc00 broadcast 10.33.3.255
	nd6 options=201<PERFORMNUD,DAD>
	media: autoselect
	status: active
    ** PAS DE PORT ETHERNET**
    
#### GATEWAY
input: **netstat -rn**
output: Destination        Gateway           
**default            10.33.3.253**
**10.33/22           link#6**
 
#### GUI - Carte IP et Infos

![](https://i.imgur.com/zpAJD7V.png)

**A quoi sert le gateway du réseau d'YNOV?**

Le Gateway sert de passerelle entre le réseau local et Internet. 

### Modification d'informations

**Modification adresse IP partie 1**


![](https://i.imgur.com/lPtCT5I.png)
 Adresse avant changement: 192.168.1.18
 Adresse après changement: 192.168.1.4
 
 Aucune déconnexion à Internet remarquée, toujours un accès fiable à Internet. 
 
 ## Partie 2
 
 ### Exploration locale en groupe

 Après avoir désactivé les firewalls et en reliant les 2 PC par câble ethernet, nous avons modifié les adresses IP pour qu'ils soient dans le même réseau local, le PC1 est en 192.168.0.1 et le PC2 est en 192.168.0.2 avec un masque en /30 ( 255.255.255.252) et pour le PC1 ( le receveur de la connexion partagée en gateway il a le pc 2 donc 192.168.0.2)
 En faisant un ifconfig on voit bien que les changements sont faits et en effectuant un ping les 2 PC se pinguent bien comme attendu.
 Résultat du ifconfig PC1 : Carte réseau Ethernet :

   Adresse IPv4. . . . . . . . . . . . . .: 192.168.0.2
   Masque de sous-réseau. . . . . . . . . : 255.255.255.252
   Passerelle par défaut. . . . . . . . . : 192.168.0.2
   
   Résultat du ipconfig PC2 : Carte réseau Ethernet :

   Adresse IPv4. . . . . . . . . . . . . .: 192.168.0.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.252
   
 Résultat du ping : Envoi d’une requête 'Ping'  192.168.0.2 avec 32 octets de données :
Réponse de 192.168.0.2 : octets=32 temps=1 ms TTL=128
Réponse de 192.168.0.2 : octets=32 temps=1 ms TTL=128
Réponse de 192.168.0.2 : octets=32 temps=1 ms TTL=128

Statistiques Ping pour 192.168.0.2:
    Paquets : envoyés = 3, reçus = 3, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 1ms, Moyenne = 1ms
    
    
 Après avoir désactivé la carte wifi du PC1, nous avons configuré le partage de connexion sur le PC2 de la façon suivante : Réseau et Internet -> "Modifier les options de l'adaptateur" -> Séléctionner la carte réseau qui partage la connexion ( carte wifi) -> "Partage" -> "Autoriser les utilisateurs du réseau à se connecter via la connexion internet de cet ordinateur" -> Selectionner par quelle carte réseau le partage se fait ( Ethernet) -> OK.
 
 Il faut changer maintenant l'adresse IP du PC1 car cette methode a changé l'IP du PC2 en 192.168.137.1

Donc on change l'IP du PC2 en 192.168.137.2/30 et en utilisant l'IP du PC2 comme gateway.

Et par ce procédé le PC1 a internet.

La commande "curl google.com" fonctionne.

En faisant un tracet -d 8.8.8.8 on trouve: Détermination de l’itinéraire vers 8.8.8.8 avec un maximum de 30 sauts.

  1     1 ms    <1 ms    <1 ms  192.168.137.1
  2     *        *        *     Délai d’attente de la demande dépassé.
  3     7 ms     7 ms    11 ms  10.33.3.253
  



- [x] **Bold**
- [ ] *Italic*
- [ ] Super^script^
- [ ] Sub~script~
- [ ] ~~Crossed~~
- [x] ==Highlight==

