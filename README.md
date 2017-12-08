# ** Prosit 2 : TCP/UDP**

## Team
 * Animateur : **Gilly**
 * Secrétaire : **Gildas**
 * Scribe : **Flo**
 * Gestionnaire : **Max**

## Mots Clés
 * Protocole TCP : Transfert Control Protocol, protocole de couche 6/7
 * Fonction "Follow TCP Stream" : Fonction de WireShark permettant de suivre une communication entre un hôte du réseau et un destinataire
 * Segment de données : Etat/PDU de l'information au niveau de la couche transport
 * Three Way Handhake : Action du protocole TCP lors de la connexion avec un autre hôte
 * Ficher WireShark
 * Adresse propre
 * Numéro de port : Numéro de la "porte" virtuelle sur laquelle "ecoute" et/ou "emet" et via lequel on est sur de le trouver
 * Application : Couche la plus haute du modèle OSI, elle possède le numéro 7
 * Accusé de réception
 * Information découpée : Action perpetree par le protocole TCP (couche 4)
 * Réassemblage
 * PDU : Protocol Data Unit

## Contexte

### Qui ?
 * Carl et le Commandant Adama

### Quoi ?
 * Etudier les données recueillit par les Cylons  
 * Comment assurer le bon acheminement des paquets
  
### Comment ?
 * En appliquant un filtre à partir de la ligne 491  
 * En utilisant le protocole TCP

### Pourquoi ?
 * Pour s'assurer de la sécurité des données

## Contraintes
 * Fichier avec un format défini

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

![Resume couches et protocoles](https://scontent-cdt1-1.xx.fbcdn.net/v/t34.0-12/24829099_2051089478504637_1961973267_n.png?oh=8755a5881940a7680b6421b077225641&oe=5A2B2886)

 * Réviser le fonctionnement de WireShark
  * Permet d'intercepter des données transitant sur un réseau et grâce à la fonction "Follow TCP Stream" de voir les données échangées entre un terminal et un autre sur Internet.
  * Avec les préfixes "GET" on visualise facilement les demande d'information/de page demandées par l'utilisateur
  * On peut mettre un filtre pour suivre uniquement une IP sur le réseau
  * [Commande pour capturer et analyser le trafic réseau](https://blog.nicolargo.com/2011/05/capturer-et-analyser-un-trafic-reseau-avec-wireshark.html)

 * Réviser le TCP/UDP
  * [Liste des Ports TCP/UDP](http://www.frameip.com/liste-des-ports-tcp-udp/)
  * TCP = Transfert Control Protocol, Utilise le Three Way Handshake, permet d'envoyer des données lourdes et de s'assurer qu'elles seront remises au destinataire  
  (Découpe les données en paquets, s'assure que le destinataire est disponible, transfère les paquets, s'assure qu'ils sont tous arrivés, permet de les remettre dans l'ordre)  
  Parfait lorsque des données doivent impérativement arriver à destination

  * UDP = User Datagram Protocol, n'utilise pas le TWH, permet d'envoyer des données de volume réduit rapidement sans se soucier de la disponibilité du destinataire et du bon acheminement des données  
  Parfait lorsque la rapidité est plus importante que la bonne arrivée des données (ex : jeux-vidéos)

  * ![Entête TCP](http://www.frameip.com/wp-content/uploads/entete-tcp-entete-tcp.gif)

  * ![Entête UDP](http://www.frameip.com/wp-content/uploads/entete-udp-entete-udp.gif)

 * TWH
  * ![Schéma Fonctionnement Three Way Handshake](https://static.lwn.net/images/2012/tfo/3whs.png)

 * OSI (*PDU, ...*)
  * Moyen mnémotechnique des couches du modèle OSI :  
  All People Seems To Need Data Processing  
  A P S T N D P  
  Application Presentation Session Transport Network(Réseau) Data(Transfert de données) Processing(Physique)

  * Application : Protocoles : FTP, Telnet, SMTP, Accès aux fichiers
  * Présentation : Conversion de fichiers, extensions des fichiers (.JPG, etc…), Extension de fichiers
  * Session : Demande de l'ouverture de session, la gère et la clos, Connexion Système
  * Transport : Découpage de l'information en **segments**, choix du protocole d'envoi de l'information, protocoles TCP / UDP
  * Réseau : Encapsulation de l'information, ajout de l'adresse IP hôte/destinataire, **paquets**, Schéma d'adressage
  * Données : Encapsulation en **trames**, ajout de l'adresse du "premier" destinataire, man in the middle like, Ensembles des règles logicielles gravé dans les circuits mémoires
  * Physique : Découpage en **bits**, transfert sur le réseau de l'information

    **Segment** = Protocole + Donnée découpée  
  **Paquet** = Adresses IP  
  **Trame** = Adresses MAC  
  **Bit** = 0 / 1

 * Socket
 Combinaison IP + Port, forme le socket et permet sur un même réseau de ne pas mélanger les hôtes demandant un accès à un service  
 C'est ce qui permet d'acheminer directement à une application des données

 * Encapsulation
 Après découpage de la donnée à transmettre, on a des segments, encapsulés en paquets, encapsulés en trames, découpées en bits  
 Ce sont les UDP de chaque couche

### Réalisation
 * Etudier le fichier WireShark

 * Déterminer les données interceptées