Bus I²C
=======

Afin de faire communiquer la raspberry pi avec tous les composants necessaires au robot (Cartes moteur, esp32, capteurs, etc) nous avons fait le choix de realiser un bus. Nous avons chercher dans un premier temps a mettre en place un bus CAN qui presentait beaucoup d'avantage interessant, malheureusement, nous n'avons pas recu a mettre en place la communication sur les cartes pilotes moteurs et sur un esp32. Nous nous sommes donc rabattu sur le bus I²C, plus commun est disponible sur beaucoup de composants mais moins robuste et moins modulable que ce nous avoins initialement prevus avec le bus CAN.




???
===


???
===



???
===




Noeud interface I²C
===================

Cette partie concerne la description du noeud qui s'occupe de la communication I²C entre la Pi et les differents composants.

Logique
*******

expliquer la structure et la logique du pgrm