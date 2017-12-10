Prosit 1.2
===================

Three Way Handshake
-------------

Le three way handshake est un protocole qui permet d'établir une connexion entre deux hôtes. Ce protocole se déroule en 3 étapes: 
>- **SYN** : le client va envoyer un paquet SYN au serveur, le paquet possède un numéro de séquence aléatoire A.
>- **SYN-ACK** : Le serveur répond au client avec un paquet SYN-ACK, le numéro du ACK est égal au numéro de séquence du paquet précédent incrémenté, et le numéro de séquence du paquet est un nombre aléatoire B.
>- **ACK** : Le client envoie un paquet ACK au serveur, ce poquet sert d'accusé de réception. Le numéro de séquence de ce paquet est la valeur reçue dans le paquet SYN-ACK (normalement A+1), et le numéro du ACK est égal au numéro de de séquence du paquet précédent (normalement B+1).

Ce protocole est souvent utilisé par le protocole TCP, car ce dernier requiert qu'une connexion soit ouverte entre les deux hôtes.

Wireshark
-------------

Wireshark est un logiciel libre et gratuit qui permet d'analyser les paquets qui transitent par la carte réseau de l'ordinateur. Il apporte une interface graphique à la commande tcpdump sous Unix.
L'application permet de décoder et de filtrer les différents paquets, elle est aussi capable de comprendre les différentes couches d'encapsulation des protocoles de communication.

TCP
-------------

Le TCP (Transmission Control Protocol) est un protocole réseau qui permet un transport fiable et sans pertes des données. Il intervient sur la couche transport du modèle OSI. Le protocole s'axe autour de 3 parties : l’établissent de la connexion (three way handshake), le transfert des données, et la fermeture de la connexion (handshaking en quatre temps).

Le protocole TCP est souvent utilisé pour l'envoie de fichier, car ce type de ressource nécessite que toutes les informations arrivent et soient mises dans le bon ordre sans pertes.

Voici la trame d'un segment TCP :
![segment TCP](http://prntscr.com/hlosio) 


UDP
-------------
L'UDP (User Datagram Protocol) est un protocole réseau qui permet un transport simple de données entre deux hôtes, chacun des deux hôtes étant défini par une adresse IP et un numéro de port. L'UPD est un protocole qui ne nécessite pas de connexion au préalable entre les deux hôtes, de ce fait les segments transmis en UDP sont soumis aux aléas du réseau : aucune garantie que le segment atteigne sa destination, ni sur l'ordre d'arrivée.
L’intégrité des données est effectuée par une somme de contrôle, mais cette dernière ne permet pas une correction des données erronées.
L'UDP est généralement utilisé pour transmettre des petites quantités de données, en général depuis un serveur vers de nombreux clients, il est par exemple très utilisé pour le streaming, les jeux en ligne ou encore la voix sur IP.

Voici la structure d'un datagramme UDP :
![enter image description here](http://prntscr.com/hlowed)


Modèle OSI
-------------

Le modèle OSI est un standard de communication informatique proposé par l'organisation mondiale de la normalisation, il décrit les fonctionnalités nécessaires à la communication entre plusieurs hôtes dans un réseau.

Il est constitué de 7 couches, chacune ayant son rôle et sa propre unité de données.

![enter image description here](http://prntscr.com/hloyyd)


Socket
-------------

Un socket est l'association d'une adresse IP et d'un numéro de port.