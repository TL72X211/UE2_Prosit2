


# Prosit 2 : TCP/UDP
Team

* Animateur : **Gilly**
* Secrétaire : **Gildas**
* Scribe : **Flo**
* Gestionnaire : **Max**

####Mots Clés

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

####Contexte
Qui ?

Carl et le Cmt Adama

Quoi ?

Etudier les données recueillit par les Cylons 
Comment assurer le bon acheminement des paquets

Comment ?

En appliquant un filtre à partir de la ligne 491
EN utilisant le protocole TCP

Pourquoi ?

Pour s'assurer de la sécurité des données

####Contraintes

* Fichier avec un format définie

####Problématique

* Comment envoyer des segments TCP tout en s'assurant de l'intégrité des données et vérifier qu'elles ont bien été reçues ?

####Généralisation

* Communication

####Hypothèses

* WireShark est un logiciel qui permet d'étudier des trames (*Emilien*)
* Follow TCP Stream est une solution permettant de récupérer les TWH (3 w handshake) (*Petit Pierre*)
* TWH sont 3 étapes nécessaires au bon fonctionnement du TCP
* La ligne 491 est le début d'un TWH (*Fantou*)

####Plan d'action
Etude

* Réviser le fonctionnement de WireShark :
	
* Réviser le TCP/UDP :
	
	Utilise tous les deux la couche transport.
	
	TCP :
		
	UDP :
		
* TWH :
	* Trois étapes :
		* SYN : le client envoi un premier paquet nommé SYN avec un numéro de séquence aléatoire au serveur.
		* SYN-ACK: le serveur répond au client avec le paquet SYN-ACK le numéro du ACK est le numéro de séquence SYN +1 alors que numéro de séquence SYN-ACK est un nombre aléatoire.
		* ACK : le client envoi le paquet ACK servant d'accusé de réception.
	* Une fois le TWH fini, une connexion full-duplex est établie.
* OSI (*PDU, ...*):
	Le modèle OSI comporte 7 couches : 
	* La couche application : concerne les applications tels que l’accès aux fichiers ainsi que leur transfert ;
	* La couche présentation : concerne la façon dont les systèmes représentent les données (encodage) ;
	* La couche session : gère la connexion entre systèmes en tenant compte de l’ordre des paquets de données et des communications ;
	* La couche transport : elle s’assure que les données ont bien été reçu ;
	* La couche réseau : fournit un schéma d’adressage ;
	* La couche liasons de données : ensemble de règles logicielles gravées dans les circuits mémoire des équipements ;
	*  La couche physique : ensemble des équipements physique permettant le transfert de données ;
	
	Chaque couche possède son propre PDU :
	* couche physique : bit ;
	* couche liaison de données : trame ;
	* couche réseau : paquet ;
	* couche transport : TPDU ;
	* couche session : SPDU ;
	* couche présentation : PPDU ;
	* couche application : APDU ;
* Socket :
	* Se situe entre la couche réseau et les couches applicatives du modèle OSI.
	* Deux modes de communication :
		* mode connecté : utilise le protocole TCP. Une communication durable est établie entre les deux processus de façon que l'adresse de destination n'est pas nécessaire à chaque envoi de données.
		* mode non connecté : utilise le protocole UDP. nécessite l'adresse de destination à chaque envoi et aucun accusé de réception n'est donné.
* Encapsulation:


Réalisation

* Etudier le fichier WireShark
* Déterminer les données interceptées

