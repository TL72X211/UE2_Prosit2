**# Prosit 2 : TCP/UDP**

  ## Team
    * Animateur : **Gilly**
    * Secrétaire : **Gildas**
    * Scribe : **Flo**
    * Gestionnaire : **Max**


## Mots Clés
   * Protocole TCP : Transmission control Protocol un des protocole principal d’internet, découpe les data en segments les transmet et les réassemble
   * Fonction "Follow TCP Stream" : filtre TCP montre les trames TCP
   * Segment de données : PDU de la couche 4 (Transport)
   * Three Way Handhake: moyen d’établir une connexion avec un hôte distant 
   * Ficher WireShark: log de tous les PDU envoyés sur le pc
   * Adresse proper: IP, MAC ?
   * Numéro de port : id permettant d’envoyer des données à un programme spécifique
   * Application 
   * Accusé de réception : pour le 3WH la ACK
   * Information découpée : on découpe les data en segments 
   * Réassemblage

  ## Contexte

  ### Qui ?
    Carl et le Cmt Adama

  ### Quoi ?
    Etudier les données recueillies par les Cylons 
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
  
t-shark sans gui
  
  * Réviser le TCP/UDP

**UDP/IP :**
IP se charge de l’adressage et UDP des ports 

Ip envoie les données d’un ordi A à un ordi B

UDP/IP envoie les données d’une appli x sur un ordi A vers une appli y sur l’ordi B

Les info d’IP acheminent le paquet vers le bon ordinateur, une fois arrivé la couche UDP délivre le paquet au bon logiciel

Problème : l’envoie de données sur internet est hasardeux, des paquets peuvent donc être perdus ou reçus en double.

**TCP à été conçu pour éviter ces problèmes :**
Il fait tout ce qu’UDP fait
Vérifie que le destinataire est prêt à recevoir des info
Découpe les gros paquets de données en petits paquet qu’IP accepte (~ 1500octets max)
Les numérote et la réception vérifie qu’ils sont tous arrivés et sinon redemande ceux manquants puis les réassemblent avant de les transmettre au logiciel et enfin envoie un accusé de réception à l’expéditeur

Si pb sur checksum (qui est dans l’en-tête) il envoie un erreur CRC
Conclusion :
TCP assure une communication fiable mais nécessite une négociation (TWH) qui prends du temps
 
 ![couches TCP](/img/1.png)
![protocoles TCP](/img/2.png)

   * Three Way Handshake

Three way handshake : selon TCP une communication entre deux hôtes s’établit en trois étapes :
1.	SYN : Le client qui désire établir une connexion avec un serveur va envoyer un premier paquet SYN au serveur, le numéro de séquence est un numéro aléatoire A
2.	SYN-ACK : le serveur répond au client avec un paquet SYN-ACK le numéro du ACK est égale au numéro de séquence du paquet SYN +1 (= A+1) et le numéro de séquence de paquet SYN-ACK est un nombre aléatoire B
3.	ACK : pour finir le client envoie au serveur un paquet ACK qui sert d’accusé de réception, son numéro de séquence est défini selon la valeur de l’acquittement reçu précédemment (A+1) et le numéro de séquence du paquet est égal à celui du SYN-ACK +1 (= B+1)

 * Ports
Numéro écris sur 2 octets ( 65 535 possibilité, le port 0 n’est pas utilisé)
7 : ICMP (echo, ping)
15 : Netstat
21 : FTP (control)
22 : SSH
23 : telnet
25 : SMTP
53 : DNS
80 : HTTP
110 : POP3
119 : NNTP (news)
123 : NTP Protocole temps réseau
137 : NBNAME service nom Netbios
139 : netbios-ssn (service de session netbios)
143 : IMAP
161 : SNMP (administration du réseau)
245 : LINK
443 : HTTPS

 * OSI (*PDU, ...*)
* Application
* Présentation
* Session
* Transport
* Réseau
* Liaison de donnée
* Physique
Comparaison OIS – TCP/IP

![osi vs tcp ip](/img/3.gif)

PDU : Protocol Data Unit
 
 ![osi](/img/4.png)
 ![osi et tcp protocoles](/img/5.jpg)
 ![osi vs tcp ip](/img/6.jpg)
    

En résumé OSI :

![couches osi](/img/7.png)
  
1.	La couche « physique » est chargée de la transmission effective des signaux entre les interlocuteurs. Son service est limité à l'émission et la réception d'un bit ou d'un train de bit continu (notamment pour les supports synchrones (concentrateur)).
2.	La couche « liaison de données » gère les communications entre 2 machines directement connectées entre elles, ou connectées à un équipement qui émule une connexion directe (commutateur).
3.	La couche « réseau » gère les communications de proche en proche, généralement entre machines : routage et adressage des paquets (cf. note ci-dessous).
4.	La couche « transport » gère les communications de bout en bout entre processus (programmes en cours d'exécution).
5.	La couche « session » gère la synchronisation des échanges et les « transactions », permet l'ouverture et la fermeture de session.
6.	La couche « présentation » est chargée du codage des données applicatives, précisément de la conversion entre données manipulées au niveau applicatif et chaînes d'octets effectivement transmises.
7.	La couche « application » est le point d'accès aux services réseaux, elle n'a pas de service propre spécifique et entrant dans la portée de la norme.

* Socket

Adresse ip : numero de port = socket
Un serveur fonctionne en écoute active sur chaque port, il le fait à l’aide de daemons qui écoutent en continu un port donné
En revanche un client ne dispose pas de port d’écoute attitré, lorsqu’il envoie une requête il spécifie donc le port sur lequel il va écouter la réponse et le serveur créé le socket approprié 
    
 * Encapsulation
 
 ![encapsulations](/img/8.png)
 ![contenu des PDU](/img/9.png)
 
Tcp : port source 16b, port desti 16b, 32b n° sequence, 32b n° ack, 4b offset (ou les data commencent), 6 b inutilisés, flag 1b par flag,16b fenetre (data avant ack), 16b checksum, 16 pointeurs
Udp : 16b port et 16 desti, 16 length, 16 checksum
Flags : urg, ack, psh, rst, syn, fin

    
### Réalisation
  * Etudier le fichier WireShark
491 SYN
503 SYN ACK
504 ACK
505 un get [https://img.youtube.com/vi/zc7utKMRjg4/1.jpg](https://img.youtube.com/vi/zc7utKMRjg4/1.jpg)
524 ACK de la transmission ligne 505
529-530 

    * Déterminer les données interceptées

[https://img.youtube.com/vi/zc7utKMRjg4/1.jpg](https://img.youtube.com/vi/zc7utKMRjg4/1.jpg)
[https://img.youtube.com/vi/zHfxgGWH8Kw/1.jpg](https://img.youtube.com/vi/zc7utKMRjg4/1.jpg)

