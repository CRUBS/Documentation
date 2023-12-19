Introduction
============

La carte d'alimentation realiser jusque la est certe fonctionelle mais est tres encombrante. il est maintenant necessaire de passer a l'etape au dessus et de realiser une carte d'alimentation professionelle. nous allons reduire la carte de la carte en utiliser des cms et en regroupant les composant. il serait bon que cette carte ne soit pas a refaire chaque année et qu'elle soit suffisement polyvalente pour repondre a tous les besoins pouvant se presenter

la realisation de cette nouvelle carte fait l'objet d'un projet lors de l'année 2023-2024



Source d'alimentation
=====================

Apres une bonne experience avec les baterie de perceuse. Nous concervons cette source d'alimentation pour les futurs robots

Afin de recuperer l'energie des batterie nous avons creer notre propre adapteur pour la batterie

nous asssurons desormais d'avoir une source d'energie fiable, facilement et rapidement rechargeable

.. image:: images/alimentation/batterie.png
   :scale: 30 %
   :align: center

Carte d'alimentation
====================

Conversion
**********

Le robot est composer de plusieurs type de carte et de composant ces derniers sont soit alimenter en 3.3V, 5V, 9V ou 12V, nous avons donc besoin de reduire la tension de la baterie a ces differents dont nous avons besoin. il existe plusieurs moyen de reduire la tension, les regulateur de tension lineaire type L7805CV feront l'affaire pour alimenter des composants peut gourmant en energie. en revanche ces derniers ne sont pas reglable est ne surporte pas toujours les besoins en courant. Il existe un second type de regulateur, les hacheurs, ces derniers fonctionnent sur le meme principe que les pwm pour abaisser la tension. ils ont l'avantage de supporter une grosse demande en courant. on utilisera aisi des lm2596 et des mini dc-dc. Les mini dc dc que nous avons choisis ont la particularité de permettre de fixer la tension de sortie ou de la regler grace a une soudure au dos du composant


.. image:: images/alimentation/buck_5a.png
   :scale: 35 %
   :align: center

.. image:: images/alimentation/mini_dcdc.png
   :scale: 35 %
   :align: center



Protection
**********


Niveau de la batterie
*********************

La tension de la batterie est image de son niveau de charge, en effet cette derniere delivre une tension de 20.5V a pleine charge et descent jusqu'a 16.5V avant d'arreter de delivrer du courant. nous avons donc besoin d'un retour du niveau de tension de la batterie.
Cette année nous decidons de changer pour afficher directement le niveau de la batterie sur la carte d'alimentation. a l'aide d'un composant, le lm3914n permet d'alimenter ou jusqu'a 10 led en fonction d'une tension qui varie sur une plage voulue



Réalisations
============



Le shema electrique
*******************



Le PCB
******


