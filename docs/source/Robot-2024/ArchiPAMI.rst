Architecture PAMIs
==================

Les PAMI anciennement PMI ont ete reintroduit cette année en remplacement du second robot. C'est derniers sont des mini robots qui interviennent en fin de match. Nous pouvons en realiser autant que nous voulons du moment que ces dernier rentrent tous dans leur zone de demarage et qu'ils font une taille minimale

cette année ces dernier ont pour objectif de rentrer en contact avec les plantes que nous avons depose. pour valider les points c'est un pami par zone et nous pouvons rentrer en contact avec le pot ou les feuille.

L'objectif est de se simplifier la vie sans reinventer tous ce qui a ete fait jusque ici. ainis concernant le controle des moteurs nous reutilisons le meme principe que pour la motorisation du robot principal. Un microcontroleur qui s'occupera des deux encodeur et des deux pwm pour les moteur.


Tout comme sur le robot
=======================

Motorisation
************

Pour comprendre les changement apporter je vous conseil de vous refere aux travaux realiser sur le robot :

- :doc:`/Robot-2024/Tree-Motorisation`

le microcontroleur utiliser est un dsPIC33CK256MP502. la differences avec celui utilser sur le robot est la nombre de module QEI ici porter a deux, ce qui permet de lire les encodeurs des deux moteur sans monter deux microcontroleur. 

le pont en h n'est pas un l298N comme sur le robot, des module hw-354 feront largement l'affaire, nous recuperons simplement le composant qui nous interesse.

Alimentation
************


Nouveautés
==========
