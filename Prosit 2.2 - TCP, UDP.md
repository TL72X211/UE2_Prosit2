*Prosit 2.2 - TCP, UDP*

# Mots Clés

- Protocole TCP
- Fonction "Follow TCP Stream"
- Segment de données
- Three Way Handshake
- Ficher WireShark
- Adresse propre
- Numéro de port
- Application
- Accusé de réception
- Information découpée
- Réassemblage

# Problématique

- *Comment envoyer des segments TCP tout en s'assurant de l'intégrité des données et vérifier qu'elles ont bien été reçues ?*

# Sommaire

### Etudes

- Fonctionnement de Wireshark
- Réviser le TCP/UDP
- TWH
- OSI
- Socket
- Encapsulation

### Réalisations

- Etudier le fichier WireShark
- Déterminer les données interceptées

# Etudes

### TCP / UDP

TPC est un protocole de transfert de données créé pour être le plus fiable possible. Les paquets envoyés avec TCP sont suivis afin qu'aucune donnée ne soit perdue ou corrompue pendant le transfert.
- Les paquets sont numérotés afin d’être reconstitué dans l’ordre.
- Le protocole demande au destinataire d’envoyer une réponse lorsque le paquet est reçu, si aucune réponse ne parvient à l’expéditeur, celui-ci pourra renvoyer le paquet.

UDP fonctionne de la même manière que TCP mais sans se préoccuper des vérifications. Il sera donc plus rapide que le TCP mais moins fiable.

### Three Way Handshake

Le Three Way Handshake est un protocole de connexion entre 2 machines. (Voir schéma)

### Socket

Un socket est une interface permettant d’acheminer les données vers un programme (= Couple IP + Port)

### Encapsulation

TCP
- 16 bits : Port Source
- 16 bits : Port Destination
- 32 bits : Numéro de Séquence
- 32 bits : Numéro ACK
-  4 bits : Offset
-  6 bits : Inutilisés
- 16 bits : Flag
- 16 bits : Checksum
- 16 bits : Pointeur
UDP
- 16 bits : Port Source
- 16 bits : Port Destination
- 16 bits : taille des données
- 16 bits : Checksum

### Modèle OSI / PDU (Révision)

Couches OSI
- Application
- Présentation = Encodage de l’info
- Session
- Transport (Assure que les données sont bien recuent) - Segments
- Réseau (Fournit un schema d’affichage) – paquets (adresses IP)
- Liaison de données (logiciels gravés dans les circuits mémoire) – trames (adresses MAC)
- Physique (Cables) - bits

Couches PDU
- Physique – Bits
- Liaison de Données – Trame (Adresse MAC)
- Réseau – Paquets (Adresse IP)
- Transport - Segments

# Réalisations

(Voir Images)
