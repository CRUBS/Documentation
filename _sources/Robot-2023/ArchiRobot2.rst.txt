Introduction
============

Objectifs
*********
Le robot n°2 sera le secondaire, il aura pour but de :

#. Ramasser les cerises disponibles sur le plateau.
#. Ranger les cerises restantes dans le panier.
#. Défendre les gâteaux montés par le robot principal.
#. Mettre les roues dans le plat, à la fin du service.
#. Se déguiser pour faire la fête.
#. Calculer l’addition.

Architecture
************

Choix d'une base diffrentielle à 2 roues de ?mm en experimentation. Le robot principal etant assez imposant, ce dernier devra etre de taille tres reduite et eviter les prehenseur qui pourraient augmenter son perimetre


Strategie CdFR
==============

strategie utiliser et deplacement sequntiel choisis pour les matchs a la cdfr

Deplacement
===========

Roue
****


Motorisation
************

utilisation des moteurs pas a pas car deja une experience

Plus d'info:

- :doc:`/Robot-2023/Tree-Motorisation`

Actionneurs
===========

Pour marquer plus de points il est possible de ramener les cerises presente dans les distributeur sur le terrain dans un panier concu par nos soins et deposé sur le board du terrain en debut de matcch.


Prehenseur des cerises
**********************

Un actionneur supplementaire a donc ete ajouter sur le cote du robot permettant de ramasser les cerises presente dans les disctributeur de cerises. les cerises sont alors amener en haut du robot dans une reserve.


Depose des cerises
******************

Nous avons rajouter une porte actionnable par un servo-moteur pour liberer les cerises prensetes dnas la reserve et les faire tomber dans le panier




Cartes
======

Raspberry pi 4
**************

Fait tourner ros2 pour faire fonctionner le robot, communique avec les autres cartes

Arduino Mega et ramps1.6
************************

Une arduino mega equipper d'un shield ramps 1.6 est utiliser uniquement pour le controle des moteurs, cette dernier recoit ces ordres par liaison serie de la pi4. elle controle aussi le relais du moteur de la remonté des cerises et le servomoteur deposant les cerises dans le panier

