**# Prosit 2 : TCP/UDP #**

  ##Team##
    * Animateur : **Gilly**
    * Secrétaire : **Gildas**
    * Scribe : **Flo**
    * Gestionnaire : **Max**


  ##Mots Clés
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

  ##Contexte

  ###Qui ?
    Carl et le Cmt Adama

  ###Quoi ?
    Etudier les données recueillit par les Cylons 
    Comment assurer le bon acheminement des paquets
  
  ###Comment ?
    En appliquant un filtre à partir de la ligne 491
    EN utilisant le protocole TCP
  
  ###Pourquoi ?
    Pour s'assurer de la sécurité des données

  ##Contraintes
    * Fichier avec un format définie

  ##Problématique
    * ~~Comment analyser un segment TCP à l'aide de WireShark ?~~
    * ~~Comment transférer des données et s'assurer qu'elles ont bien été reçues ?~~
    * Comment envoyer des segments TCP tout en s'assurant de l'intégrité des données et vérifier qu'elles ont bien été reçues ?

  ##Généralisation
    * Communication

  ##Hypothèses
    * WireShark est un logiciel qui permet d'étudier des trames (*Emilien*)
    * Follow TCP Stream est une solution permettant de récupérer les TWH (3 w handshake) (*Petit Pierre*)
    * TWH sont 3 étapes nécessaires au bon fonctionnement du TCP
    * La ligne 491 est le début d'un TWH (*Fantou*)

  ##Plan d'action

  ###Etude
    * Réviser le fonctionnement de WireShark
    * Réviser le TCP/UDP
    * TWH
    * OSI (*PDU, ...*)
    * Socket
    * Encapsulation
    
  ###Réalisation
    * Etudier le fichier WireShark
    * Déterminer les données interceptées
