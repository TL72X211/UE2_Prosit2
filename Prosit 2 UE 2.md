Prosit 2 : TCP/UDP

Team

    Animateur : Gilly
    Secrétaire : Gildas
    Scribe : Flo
    Gestionnaire : Max

####Mots Clés

    Protocole TCP
    Fonction "Follow TCP Stream"
    Segment de données
    Three Way Handhake
    Ficher WireShark
    Adresse propre
    Numéro de port
    Application
    Accusé de réception
    Information découpée
    Réassemblage

####Contexte Qui ?

Carl et le Cmt Adama

Quoi ?

Etudier les données recueillit par les Cylons Comment assurer le bon acheminement des paquets

Comment ?

En appliquant un filtre à partir de la ligne 491 EN utilisant le protocole TCP

Pourquoi ?

Pour s'assurer de la sécurité des données

####Contraintes

    Fichier avec un format définie

####Problématique

    Comment envoyer des segments TCP tout en s'assurant de l'intégrité des données et vérifier qu'elles ont bien été reçues ?

####Généralisation

    Communication

####Hypothèses

    WireShark est un logiciel qui permet d'étudier des trames (Emilien)
    Follow TCP Stream est une solution permettant de récupérer les TWH (3 w handshake) (Petit Pierre)
    TWH sont 3 étapes nécessaires au bon fonctionnement du TCP
    La ligne 491 est le début d'un TWH (Fantou)

####Plan d'action Etude

* Réviser le fonctionnement de WireShark :

* Réviser le TCP/UDP :
	>* UDP :
		User Datagram Protocol est un des principaux protocoles de télécommunication utilisés par internet. Il fait partie de la couche transport du modèle OSI. Il est détaillé dans la RFC 768. Son rôle est de permettre la transmission de données de manière simple entre deux entités. Aucune communication préalable n'est requise afin d'établir la connexion, UDP utilise un mode de transmission sans connexion. L'intégrité des données est assuré par la somme de contrôle sur l'en-tête. Cette somme est obligatoire en IPv6.
		Propriétés de l'UDP: 
		- orienté transaction;
		- fournit des datagrammes;
		- simple donc adapté pour le bootstrapping;
		- sans état;
		- absence de délai de retransmission en fait un protocole utile pour les applications en temps réel;
		- fonctionne efficacement dans des communications unidirectionnelles donc est adapté à la diffusion d'informations;
		Structure du datagramme:
			Le paquet UDP est encapsulé dans un paquet IP et comporte un en-tête suivi des données à transporter.
			L'en-tête du datagramme UDP est composé du :
				- Port source qui indique depuis quel port le paquet est envoyé;
				- Port de destination indiquant sur quel port le paquet doit être envoyé;
				- Longueur qui indique la longueur totale du segment UDP. La longueur minimale est de 8 octets;
				- Somme de contrôle permet de s'assurer de l'intégrité du paquet reçu quand elle est différente de 0;
	>* TCP : 
		Protocole de transport fiable en mode connecté dans la RFC 793 de l'IETF. Dans le modèle internet, TCP est au-dessus de IP. Dans le modèle OSI cela correspond à la couche transport. Pour se connecter il utilise le Three Way Handshake.
		Le segment TCP est composé de :

				- Port source : numéro du port source
				- Port destination : numéro du port destination
				- Numéro de séquence : numéro de séquence du premier octet de ce segment
    - Numéro d'acquittement : numéro de séquence du prochain octet attendu
    - Taille de l'en-tête : longueur de l'en-tête en mots de 32 bits (les options font partie de l'en-tête)
    - Indicateurs ou Flags :
		* Réservé : réservé pour un usage futur
		* ECN/NS : signale la présence de congestion, voir RFC 31683 ; ou Nonce Signaling, voir RFC 35404
		* CWR : Congestion Window Reduced : indique qu'un paquet avec ECE a été reçu et que la congestion a été traitée
		*  ECE : ECN-Echo : si SYN=1 indique la capacité de gestion ECN, si SYN=0 indique une congestion signalée par IP (voir RFC 3168)
		* URG : Signale la présence de données urgentes
		* ACK : signale que le paquet est un accusé de réception (acknowledgement)
		* PSH : données à envoyer tout de suite (push)
		* RST : rupture anormale de la connexion (reset)
		* SYN : demande de synchronisation ou établissement de connexion
		* FIN : demande la fin de la connexion
	- Fenêtre : taille de fenêtre demandée, c'est-à-dire le nombre d'octets que le récepteur souhaite recevoir sans accusé de réception
	- Somme de contrôle : somme de contrôle calculée sur l'ensemble de l'en-tête TCP et des données, mais aussi sur un pseudo en-tête (extrait de l'en-tête IP)
	- Pointeur de données urgentes : position relative des dernières données urgentes
	- Options : facultatives
	- Remplissage : zéros ajoutés pour aligner les champs suivants du paquet sur 32 bits, si nécessaire
	- Données : séquences d'octets transmis par l'application (par exemple : +OK POP3 server ready...)
	
* TWH :
        Trois étapes :
            SYN : le client envoi un premier paquet nommé SYN avec un numéro de séquence aléatoire au serveur.
            SYN-ACK: le serveur répond au client avec le paquet SYN-ACK le numéro du ACK est le numéro de séquence SYN +1 alors que numéro de séquence SYN-ACK est un nombre aléatoire.
            ACK : le client envoi le paquet ACK servant d'accusé de réception.
        Une fois le TWH fini, une connexion full-duplex est établie.

* OSI (PDU, ...): Le modèle OSI comporte 7 couches :
        La couche application : concerne les applications tels que l’accès aux fichiers ainsi que leur transfert ;
        La couche présentation : concerne la façon dont les systèmes représentent les données (encodage) ;
        La couche session : gère la connexion entre systèmes en tenant compte de l’ordre des paquets de données et des communications ;
        La couche transport : elle s’assure que les données ont bien été reçu ;
        La couche réseau : fournit un schéma d’adressage ;
        La couche liasons de données : ensemble de règles logicielles gravées dans les circuits mémoire des équipements ;
        La couche physique : ensemble des équipements physique permettant le transfert de données ;

    Chaque couche possède son propre PDU :
       - couche physique : bit ;
       - couche liaison de données : trame ;
       - couche réseau : paquet ;
       - couche transport : TPDU ;
       - couche session : SPDU ;
       - couche présentation : PPDU ;
       - couche application : APDU ;
* Socket :
        Se situe entre la couche réseau et les couches applicatives du modèle OSI.
        Deux modes de communication :
           - mode connecté : utilise le protocole TCP. Une communication durable est établie entre les deux processus de façon que l'adresse de destination n'est pas nécessaire à chaque envoi de données.
           - mode non connecté : utilise le protocole UDP. nécessite l'adresse de destination à chaque envoi et aucun accusé de réception n'est donné.

* Encapsulation:

Réalisation

    - Etudier le fichier WireShark
    - Déterminer les données interceptées
