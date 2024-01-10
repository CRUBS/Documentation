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

Choix d'une base différentielle à 2 roues de ?mm en expérimentation. Le robot principal étant assez imposant,
ce dernier devra donc être de taille très réduite. Il faut donc éviter les préhenseurs qui pourraient augmenter
son périmètre.


Stratégie CdFR
==============

Stratégie utilisée et déplacement séquentiel choisis pour les matchs à la CDFR.

Déplacement
===========

Roue
****


Motorisation
************

Utilisation des moteurs pas à pas, car déjà une expérience.

Plus d'info:

- :doc:`/Robot-2023/Tree-Motorisation`

Actionneurs
===========

Pour marquer plus de points, il est possible de ramener les cerises présentes dans les distributeurs sur le terrain
dans un panier conçu par nos soins et déposé sur le bord du terrain en début de match.


Préhenseur des cerises
**********************

Un actionneur supplémentaire a donc été ajouté sur le côté du robot permettant de ramasser les cerises présentes
dans les distributeurs de cerises. Les cerises sont alors amenées en haut du robot dans une réserve.


Dépose des cerises
******************

Nous avons rajouté une porte actionnable par un servomoteur pour libérer les cerises présentes dans la réserve
et les faire tomber dans le panier.




Cartes
======

Raspberry pi 4
**************

Fait tourner ROS2 pour faire fonctionner le robot, communique avec les autres cartes.

Arduino Mega et ramps1.6
************************

Une Arduino méga équiper d'un shield *ramps 1.6* est utilisé uniquement pour le contrôle des moteurs,
cette dernière reçoit ces ordres par liaison série de la Pi. Elle contrôle aussi le relais du moteur
lors de la remonté des cerises et le servomoteur déposant les cerises dans le panier.
