Bus I²C
=======

Afin de faire communiquer la raspberry pi avec tous les composants necessaires au robot (Cartes moteur, esp32, capteurs, etc) nous avons fait le choix de realiser un bus. Nous avons chercher dans un premier temps a mettre en place un bus CAN qui presentait beaucoup d'avantage interessant, malheureusement, nous n'avons pas recu a mettre en place la communication sur les cartes pilotes moteurs et sur un esp32. Nous nous sommes donc rabattu sur le bus I²C, plus commun est disponible sur beaucoup de composants mais moins robuste et moins modulable que ce nous avoins initialement prevus avec le bus CAN.




???
===


Carte electronique
==================

Afin de simplifier les connections nous avons réaliser une carte avec un bornier de connecteur dupont, une ligne ground, une ligne SCL et un SDA. sur la meme carte nous avons rajouter deux PCF8574 et la possibilité de choisir leur adresses. Ces composants rajoutent 8 sorties digitales dont il est possible de controller l'etat des sorties a partir d'un bytes (8 bits, une par sortie).


Composants sur le bus
=====================

Voici la liste des composants presents sur le bus I²C que nous avons mis en place :

PCF8574
*******

Il est possible de modifier l'adresses des PCF8574 grace aux jumper a souder disponible a l'arriere de la carte. Ils sont actuellement aux adresses 0x20, 0x21

Cartes moteurs
**************

Les 2/3 cartes moteurs sont presentes sur le bus I²C aux adresses 0x51, 0x52 et 0x53.


ESP32
*****


Imu
***

l'IMU permetant de recuperer les informations des mouvements du robot est a l'adresse 0x??

Capteurs temps de vol VL53L0X
*****************************

Les capteur tof (time of flight) present sur le robot permettent de detecter les PAMI, ils sont par defaut à l'adresse 0x29 mais il est possible de changer leur adresse pour en mettre plusieurs sur le meme bus. voici les etapes :

**TODO**


Ecran LCD 2004
**************

0x27





Noeud interface I²C
===================

Cette partie concerne la description du noeud qui s'occupe de la communication I²C entre la Pi et les differents composants.

Logique
*******

expliquer la structure et la logique du pgrm