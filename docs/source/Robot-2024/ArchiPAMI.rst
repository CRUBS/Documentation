Architecture PAMIs
==================

Les PAMIs anciennement PMIs ont été réintroduit cette année en remplacement du second robot. Ces derniers sont des mini
robots qui interviennent en fin de match. Nous pouvons en réaliser autant que nous voulons du moment que ces derniers
rentrent tous dans leur zone de démarrage et qu'ils font une taille minimale.

Cette année ces derniers ont pour objectif de rentrer en contact avec les plantes que nous avons déposées. Pour valider
les points, c'est un PAMI par zone et nous pouvons rentrer en contact avec le pot ou les feuilles.

L'objectif est de se simplifier la vie sans réinventer tout ce qui a été fait jusqu’ici. Ainsi concernant le contrôle
des moteurs nous réutilisons le même principe que pour la motorisation du robot principal. Un microcontrôleur
qui s'occupera des deux encodeurs et des deux PWM pour le pont en H des moteurs.


Tout comme sur le robot
=======================

Motorisation
************

Pour comprendre les changements apportés je vous conseille de vous référer aux travaux réaliser sur le robot :

- :doc:`/Robot-2024/Tree-Motorisation`

Le microcontrôleur utilisé est un dsPIC33CK256MP502. La différence avec celui utilisé sur le robot est le nombre
de modules QEI (Quadrature Encoder Interface) ici porté à deux, ce qui permet de lire les encodeurs des deux moteurs
sans monter deux microcontrôleurs.

Le pont en H n'est pas un l298N comme sur le robot, des modules hw-354 feront largement l'affaire, nous récupérons
simplement le composant qui nous intéresse.

Alimentation
************


Nouveautés
==========
