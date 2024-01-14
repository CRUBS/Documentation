Introduction
============

La carte d'alimentation réalisée jusque là est certes fonctionelle mais est très encombrante. Il est maintenant
nécessaire de passer à l'étape au-dessus et de réaliser une carte d'alimentation plus professionnelle.
Nous allons réduire la carte de la carte en utilisant des composants CMS et en regroupant les composants. Il serait
bon que cette carte ne soit pas à refaire chaque année et qu'elle soit suffisamment polyvalente pour répondre à
tous les besoins pouvant se presenter.

La réalisation de cette nouvelle carte fait l'objet d'un projet lors de l'année 2023-2024.

Sources d'alimentation
======================

Batterie
********

Apres une bonne expérience avec les batteries de perceuse. Nous conservons cette source d'alimentation pour les futurs
robots.

Afin de récupérer l'énergie des batteries, nous avons créé notre propre adaptateur pour la batterie.

Nous asssurons désormais d'avoir une source d'énergie fiable, facilement et rapidement rechargeable.

.. image:: images/alimentation/batterie.png
   :scale: 30 %
   :align: center

Alim externe
************

Nous faisons désormais en sorte que le robot puisse être alimenté par une alimentation externe
(les alims stabilisées de labo) pour ne pas vider les batteries de perceuse inutilement.


Choix de l'alim
***************

Le robot pouvant être alimenté soit par une batterie soit par une alim externe, nous rajoutons un interrupteur
permettant de sélectionner la source d'alimentation.

.. ajouter la carte 



Carte d'alimentation
====================

Conversion
**********

Le robot est composé de plusieurs types de carte et de composants. Ces derniers sont alimentés sous différentes tensions
(en 3.3V, 5V, 9V ou 12V). Nous avons donc besoin de réduire la tension de la batterie à ces différentes tensions
dont nous avons besoin. Il existe plusieurs moyens de réduire la tension, les régulateurs de tension linéaires
type L7805CV feront l'affaire pour alimenter des composants peu gourmands en énergie. En revanche, ces derniers ne sont
pas réglables est ne supporte pas toujours les besoins en courant. Il existe un second type de régulateur, les hacheurs,
ces derniers fonctionnent sur le même principe que les PWM pour abaisser la tension. Ils ont l'avantage de supporter
une grosse demande en courant. On utilisera aussi des lm2596 et des mini buck-converter.


.. image:: images/alimentation/buck_5a.png
   :scale: 35 %
   :align: center

.. image:: images/alimentation/mini_buck.png
   :scale: 50 %
   :align: center



Protection
**********

Entre nous ... on fout une diode 6 Ampères avant la carte d'alimentation et c'est protégé non ? Et comme on est motivé,
on rajoute un fusible reformable par sortie et un fusible 5A en entrée de la carte pour la forme :)


Niveau de la batterie
*********************

La tension de la batterie est image de son niveau de charge, en effet cette dernière délivre une tension de 21V à pleine
charge et descend jusqu'à 16.5V avant d'arrêter de délivrer du courant. Nous avons donc besoin d'un retour du niveau
de tension de la batterie.

Cette année nous décidons de changer pour afficher directement le niveau de la batterie sur la carte d'alimentation.
À l'aide d'un composant, le lm3914n permet d'alimenter ou jusqu'à 10 LED en fonction d'une tension qui varie sur
une plage voulue.

Réalisations
============

La carte comporte donc :

* le connecteur d'entrée de tension
* le connecteur pour le bouton d'alimentation
* le connecteur pour l'arrêt d'urgence, notez que l'arrêt d'urgence ne coupe pas la Pi et l'ESP32
* le retour d'un niveau de batterie
* un buck converter 12V 5A pour les 3 sorties moteurs
* un buck converter 5V 5A pour la Pi (non coupé par l'AU)
* un buck converter 9V 3A pour l'ESP32 (non coupé par l'AU)
* deux buck converter 5V 3A pour 2*10 sorties
* un buck converter 9V 3A pour 10 sorties
* un buck converter 3.3V 3A pour 10 sorties
* un buck converter 12V 3A pour 10 sorties



Le schéma électrique
********************



Le PCB
******


