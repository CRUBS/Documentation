Introduction
============

Cette page est dédiée aux améliorations du mât de repérage du robot et donc du lidar. Je vous renvoie vers l'article
concernant les informations du lidar (installation, référence, etc.) :

:doc:`/Robot-2023/Tree-Lidar`

Pendant l'édition 2023 de la coupe, nous avons eu plusieurs idées permettant d'amélioration le mât :

#. Hauteur de la plateforme dédiée à l'équipe adverse réglable
#. Cacher le socle du lidar, car ce dernier ne scan pas
#. Ajouter un cercle de LED autour du lidar et coder une visualisation des informations perçues par le lidar sur ce cercle.

Ces 3 points font l'objet d'un projet pour l'année 2023-2024


Améliorations
=============

Structure
*********






LEDs
****

La référence des LEDs est un anneau de WS2812b, ce sont des LEDs "adressables", des LEDs RGB dont on peut contrôler
la couleur individuellement.

.. image:: images/lidar/anneau_leds.png
   :scale: 60 %
   :align: center

Ce genre de ruban LED peut normalement être commandé par une Raspberry, mais après beaucoup de temps passé dessus,
nous n'avons pas réussi depuis Ubuntu 22.04 (alors que nous avons réussi sur Raspbian). Nous faisons donc le choix
de piloter les LEDs depuis l'ESP32 et les informations du lidar seront transmises de la PI à l'esp32 sur le bus I²C.



