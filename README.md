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
* TWH
* OSI (*PDU, ...*)
* Socket
* Encapsulation
    
  ### Réalisation
* Etudier le fichier WireShark
* Déterminer les données interceptées


### Révision de WireShark
--

### Réviser le TCP/UDP

Les deux protocoles appartiennent à la couche Tranposrt (4) du modèle OSI

#### UDP
  UDP (User Datagram Protocol) est un protocole d'acheminement de paquets, combiné avec l'IP il peut trouver la machine à laquelle il doit délivrer les données.
  Ce protocole utilise un mode de transmission sans connexion. L'intégrité de ces données est assurée par une somme de contrôle dans son en-tête.
  Ce protocole expose le programme qui l'utilise aux problèmes éventuels de fiabilité du réseau ; ainsi, il n'existe pas de garantie de protection quant à la livraison, l'ordre d'arrivée, ou la duplication éventuelle des datagrammes.
  ![](https://image.prntscr.com/image/4i6CNSKzSbiRXTppOtJ0hg.png)
  ![](https://image.prntscr.com/image/7Qkyu5SMSMa85SIFeLPDfQ.png)
  
#### TCP

Le TCP a son inverse est un protocole qui utilise un mode de transmission avec connexion (Three Way Handshake)

![](https://image.prntscr.com/image/ocsktJyDTN6mWfYyGMgmxA.png)


#### Three Way Handshake

Un Three-Way Handshake(TWH) est une méthode utilisée dans un réseau TCP / IP pour créer une connexion entre un hôte / client local et un serveur. Il s'agit d'une méthode en trois étapes qui nécessite que le client et le serveur échangent des paquets SYN et ACK (acknowledgment) avant le début de la communication de données.

* Un client envoie un paquet de données SYN sur un réseau IP à un serveur sur le même réseau ou sur un réseau externe. L'objectif de ce paquet est de demander / infer si le serveur est ouvert pour de nouvelles connexions.
* Le serveur cible doit avoir des ports ouverts pouvant accepter et initialiser de nouvelles connexions. Lorsque le serveur reçoit le paquet SYN du client, il répond et renvoie un accusé de réception - le paquet ACK ou le paquet SYN / ACK.
* Le client reçoit le SYN / ACK du serveur et répond avec un paquet ACK.


#### OSI

![](https://alln-extcloud-storage.cisco.com/ciscoblogs/osi-550x425.gif)


#### Socket

Un socket est la combinaison de l'adresse IP et le port
Par exemple : 192.168.1.1:33548


#### Encapsulation

![](http://www.routemybrain.com/wp-content/uploads/2010/04/encapsulation.jpg)
