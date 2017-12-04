**# Prosit 2 : TCP/UDP**

  ## Team
    * Animateur : **Gilly**
    * Secrétaire : **Gildas**
    * Scribe : **Flo**
    * Gestionnaire : **Max**


  ## Mots Clés
    * Protocole TCP : Transmission Control Protocol
    * Fonction "Follow TCP Stream" : Fonction disponible sous Wireshark pour suivre un flot de données.
    * Segment de données : Portion d’espace d’adressage virtuel d’un programme. Il contient les variables globales et statiques déclarés par le programmeur. C’est ce qui va servir au « sergment code ».
    * Three Way Handhake :
    ![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/1.png)
    * Fichier WireShark :
    * Adresse proper : L’adresse propre, l’adresse correcte.
    * Numéro de port : Permet sur un ordinateur de distinguer les différents programmes informatiques qui écoutent ou émettent des informations sur des ports. On distingue un port par son numéro. Ce sont des portes qui donnent accès au système d’exploitation. Un numéro de port est codé sur 16 bits, soit 2^16 => 65536 ports distincts.
- 0 à 1023 -> Services réseaux les plus courant
- 1024 à 49151 -> Ports enregistrés par l’IANA
- 49152 à 65535 -> Ports dynamiques utilisable pour tout type de requêtes TCP ou UDP
    * Application : Programme (ou ensemble logiciel) directement utilisé pour réaliser une tâche, ou un ensemble de tâches élémentaires d’un même domaine ou formant un tout.
    * Accusé de réception : Message confirmant l’arrivé la réception d’un message.
    * Information découpée :
    * Réassemblage :

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
    * ~Comment analyser un segment TCP à l'aide de WireShark ?~
    * ~Comment transférer des données et s'assurer qu'elles ont bien été reçues ?~
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


**1 – TCP**

Protocole IP -> @source + @destination + @port

Protocole TCP ->
- Vérifie que le destinataire est prêt à recevoir les données
- Découper les gros paquets de données en plus petits pour que IP les accepte
-	Numéroter les paquets, et à la réception de vérifier qu’ils sont tous bien arrivés, de redemander les paquets manquants, réassembler avant de les donner aux logiciels.
-	S’occupe de la génération pour vérifier que les données sont bien arrivées.
 ![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/2.png)
@Port source [16 bits] -> Port source de la machine qui envoi
@Port destination[16bits] port relatif à l’application en cours, sur la machine de destination.
@Numéro de séquence [32 bits] numéro du paquet. Permet de réassembler à la fin, et de placer le paquet à la bonne place.
@numéro d’ACK[32 bits] Signale le prochain numéro de paquet attendu.
@Offset [4 bits] : Indique où les données commencent.
@Réservé [6 bits] :  Pour le futur
@Flags : 
-	URG : Champ pointeur de données urgente
-	ACK : indique que le numéro de séquence pour la confirmation est valide
-	PSH : Indique au récepteur de délivrer les données à l’application, et de ne pas attendre que les tampons soient remplis.
-	RST : Demande la réinitialisation de la connexion.
-	SYN : indique la synchronisation des numéros de séquence
-	FIN : Fin de transmission
@Fenêtre [16 bits] : Correspond au nombre d’octets à partir de la position marquée dans l’accusé de réception que le récepteur est capable de recevoir. L’envoyeur va donc s’appuyer dessus pour ne pas le submerger.
@Checksum [16 bits] : Représente la validité du paquet de la couche 4 TCP
@Pointeur[16 bits] : communique la position d’une donnée urgente en donnant son décalage par rapport au numéro de séquence.
On peut aussi ajouter des options.


Il utilise les « Three way handshake” pour opérer entre un client et un serveur. De même, lors de la fermeture de données, il utilisera un message particulier.
 ![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/3.png)


La fenêtre coulissante ou « Sliding Windows » définit le volume de données susceptible d’être passées via une connexion TCP avant que le récepteur n’envoie un accusé de réception.

Avantage du TCP : 
-	Communication rapide
-	Convient pour un transfert d’un nombre moyen ou d’un grand volume de données
-	Possibilités de routage
-	Acquittement
Inconvénients :
-	Peut seulement transmettre des données de longueurs statiques
-	Charge de travail de programmation augmentée pour la gestion de données
-	Les données sont transmises par flux

TCP est utilisé : Navigateurs (avec http), FTP, SMT3 et POP3, peut marcher avec le DNS.
**2 – UDP **
 ![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/4.png)

@Port UDP [16 bits] : Port relatif à l’application source
@Port Destination[16 bits] : Port relatif à l’application sur la machine à distance.
@Longeur [16 bits] : Taille de l’entête et des données.
@Checksum [16 bits] : représente la validité du paquet de la couche 4.

Avantages : 
-	Transmission de données très rapide
-	Très flexible, utilisable facilement avec les systèmes tiers
-	Routable
-	Fonctionnalités Multicast / Broadcast
-	Adapté pour des petites jusqu’à moyenne quantités de données ( < 2048 Octets)
Inconvénients :
-	Paquets perdus ne sont pas renvoyés
-	Paquets de données avec une somme de contrôle fausse sont rejetés et ne sont pas redemandés
-	Des délivrances multiples de paquets séparés sont possibles
-	L’ordre d’arrivée des paquets chez le récepteur ne peut pas être prévu
-	Des données sont transmises orientés paquets
-	Fonction broadcast seulement utilisable en émission



**3 – Les sockets / Ports**

Quand on fait @IP + Port => Socket : Permet d’identifier le service qui est connecté sur une machine connectée.
NAT (Network Address Translation) : Faculté dont dispose un routeur, de modifier les @IP des émetteurs, lors du passage des datagrammes entre deux réseaux.
PAT (Port Access Translation) : Permet de changer au passage le numéro de port dans le datagramme.
MASQUERADE : Mélange entre le NAT et le PAT, peut connecter tout un réseau local construit sur une @IP privée d’internet.
Les ports à connaître :
  ![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/5.png)


**4 – Le modèle TCP/IP – OSI – DataType**
![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/6.png)
![](https://github.com/TL72X211/UE2_Prosit2/blob/Emilien/Screens_Prosit/7.png)
 
**5 – Wireshark**
En analysant les trames TCP, à l’heure indiqué, on trouve des images de vidéos YouTube.
Voici un des liens :
https://www.youtube.com/watch?v=zHfxgGWH8Kw

