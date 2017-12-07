**# Prosit 2 : TCP/UDP**

## Team
* Animateur : **Gilly**
* Secrétaire : **Gildas**
* Scribe : **Flo**
* Gestionnaire : **Max**


## Mots Clés
* Protocole TCP
* Fonction "Follow TCP Stream"
* Segment de données
* Three Way Handhake
* Ficher WireShark
* Adresse propre
* Numéro de port
* Application
* Accusé de réception
* Information découpée
* Réassemblage

## Contexte

### Qui ?
    Carl et le Cmt Adama

### Quoi ?
    Etudier les données recueillit par les Cylons 
    Comment assurer le bon acheminement des paquets
  
### Comment ?
    En appliquant un filtre à partir de la ligne 491
    EN utilisant le protocole TCP
  
### Pourquoi ?
    Pour s'assurer de la sécurité des données

## Contraintes
* Fichier avec un format définie

## Problématique
* ~~Comment analyser un segment TCP à l'aide de WireShark ?~~
* ~~Comment transférer des données et s'assurer qu'elles ont bien été reçues ?~~
* Comment envoyer des segments TCP tout en s'assurant de l'intégrité des données et vérifier qu'elles ont bien été reçues ?

## Généralisation
* Communication

## Hypothèses
* WireShark est un logiciel qui permet d'étudier des trames (*Emilien*)
* Follow TCP Stream est une solution permettant de récupérer les TWH (3 w handshake) (*Petit Pierre*)
* TWH sont 3 étapes nécessaires au bon fonctionnement du TCP
* La ligne 491 est le début d'un TWH (*Fantou*)

## Plan d'action

### Etude
* Réviser le fonctionnement de WireShark
* Réviser le TCP/UDP

TCP et UDP sont 2 protocoles de la couche transport du modèle OSI. Ils servent à échanger des paquets d'information entre 2 machines en utilisant leur adresse IP et un numéro de port.

Le protocole TCP doit d'abord se connecter à la machine distante avec un "Three Way Handshake". Une fois fait, les 2 machines peuvent communiquer de manière bidirectionnelle. Tant qu'on ne ferme pas la connexion, les 2 machines peuvent s'échanger des paquets.
On appelle ce protocole "protocole orienté connexion" car il a besoin de se connecter pour échanger des paquets.
Le TCP sert de base pour beaucoup d'autres protocoles de plus haut niveau (HTTP, FTP, POP3, IMAP, SMTP etc...). FCP nous permet de vérifier l'intégrité des paquets à l'arrivé ainsi que l'envoie d'accusé de réception à la fin d'un envoie. Cela permet donc de vérifier qu'aucuns paquets ne se soit perdu dans l'échange. Il renvoie les paquets qui se sont perdus.

A l'inverse le protocole UDP est un "protocole orienté sans connexion". Il n'a pas besoin de se connecter pour envoyer ses paquets. Il suffit juste de renseigner dans le paquet l'ip et le port de la destination puis de l'envoyer. Il ne fournit aucune vérification pour la réception des données. Il n'y a ni accusé de reception, ni numéro d'identification de paquet.
Il permet d'être beaucoup plus rapide que le TCP. Lui aussi sert de base pour d'autres protocoles de plus haut niveau (DNS, BOOTPS, DHCP, TFTP, SNMP ). On l'utilise souvent dans le stream, la voIP ou le stream car même si l'on pert un paquet ce n'est pas pas dérangeant (et la plus part du temps non visibile par nos sens). 


Voici les entête des paquets TCP et UDP :

![entêteTcpUdp](http://www.highteck.net/images/51-TCP-UDP-Header.jpg)
* TWH

Le Three Way Handshake permet la création d'une connexion entre un client et un serveur. Il s'effectue dans une communication TCP. Il y a 3 étapes pour créer une connexion :

- **SYN** : Le client qui désire établir une connexion avec un serveur va envoyer un premier paquet SYN (synchronized) au serveur. Le numéro de séquence de ce paquet est un nombre aléatoire A
- **SYN-ACK** : Le serveur va répondre au client à l'aide d'un paquet SYN-ACK (synchronize, acknowledge). Le numéro du ACK est égal au numéro de séquence du paquet précédent (SYN) incrémenté de un (A + 1) tandis que le numéro de séquence du paquet SYN-ACK est un nombre aléatoire B.
- **ACK** :  Pour terminer, le client va envoyer un paquet ACK au serveur qui va servir d'accusé de réception. Le numéro de séquence de ce paquet est défini selon la valeur de l'acquittement reçu précédemment (par exemple : A + 1) et le numéro du ACK est égal au numéro de séquence du paquet précédent (SYN-ACK) incrémenté de un (B + 1).

La connexion etablie est une communication full-duplex.

![Three_Way_Handshake](http://www.mdpi.com/applsci/applsci-06-00358/article_deploy/html/images/applsci-06-00358-g001.png)

* OSI (*PDU, ...*)

![schéma_Osi_Pdu](https://user.oc-static.com/files/284001_285000/284769.png)

* Socket

Un socket est un constitué d'une adresse ip est d'un port. Ex: 194.2.77.162:80

* Encapsulation

![schéma_encapsulation](http://www.firewall.cx/images/stories/osi-encap-decap-1.gif)

    
### Réalisation
* Etudier le fichier WireShark
* Déterminer les données interceptées

Si on utilise le filtre "Follow TCP Stream" on voit plusieurs URL apparaître. Si on suit les liens, on trouve des images et des vidéos youtubes.
