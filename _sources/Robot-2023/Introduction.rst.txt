Sujet
=====

Joyeux anniversaire la Coupe de Robotique ! Grand-mère Monique souhaite célébrer cette grande occasion en préparant des gâteaux pour tout le monde. Elle demande à ce que vous l’aidiez à préparer sa recette légendaire et à ce que tous les invités soient servis.

.. image:: images/logo_cdfr_2023.png
	:scale: 40 %
	:align: center

Génoise, crème, glaçage et sans oublier la fameuse cerise, voilà de quoi cuisiner pour réjouir Grand-mère Monique. À vos cuillères !

Ces missions seront :

#. Faire des gâteaux.
#. Mettre les cerises sur les gâteaux.
#. Ranger les cerises restantes dans le panier.
#. Mettre les roues dans le plat, à la fin du service.
#. Se déguiser pour faire la fête.
#. Calculer l’addition.

.. image:: images/plateau_cdfr_2023.png
	:scale: 80 %
	:align: center

Choix
=====

Généralités
***********

Nous tentons de faire deux robots cette année.
Nous préparons un robot principal, durable dans les années. Le but étant de ne pas avoir à concevoir un nouveau robot chaque année.

Préhenseurs
***********

Le robot principal sera l'équipe d'un élévateur conçu une fois. L'objectif et de garder le principe de l'élévateur du préhenseur et de simplement changer l'outil de préhension en s'adaptant au sujet de chaque année. Cet élévateur sera en test sur le robot 1.

Alimentation
************

Mes cartes d'alimentation pour les deux robots.
Leger retravaille de l'alimentation de l'année passée, pas beaucoup de changements :

- :doc:`/Robot-2023/Tree-Alimentation`

Motorisation
************

Toujours dans l'idée de gagner du temps, nous avons fait le choix de conserver les moteurs pas à pas, car nous avions déjà un code existant pour les utiliser sur les deux robots. En cours d'années, nous avons quand même dû refaire entièrement le code de contrôle des moteurs.

- :doc:`/Robot-2023/Tree-Motorisation`


Détection d'obstacle
********************

Dans un premier temps, nous avons lancé deux membres du club sur le développement d'un système de détection.
Le principe était d'utiliser les 3 mâts présents sur les bords du plateau comme émetteur infrarouge et équipe les robots adverses comme allié des cartes réceptrices. Les cartes émettrices étaient équipées de plusieurs LEDs infrarouges disposées en cercle, ces dernières émettaient chacune leur tour un code correspondant à leur numéro. Les cartes réceptrices sont équipées avec plusieurs récepteurs infrarouges disposés en cercle, ce qui permettait de détecter quel récepteur captait quels LEDs infrarouges ce qui permettait de trianguler les robots.

Les résultats ont malheureusement montré une faible précision, plaçant les robots avec une imprécision allant de 2cm à 15cm près ce qui n'était pas concevable

Nous avons donc en cours d'année fait l'acquisition de lidar avec des paquets déjà disponible pour ros2:

- :doc:`/Robot-2023/Tree-Lidar`

Robot n°1 PI
============

- :doc:`/Robot-2023/Tree-ArchiRobot1`

Objectifs
*********
Le robot n°1 sera le principal, il aura pour but de :

#. Faire les gâteaux.
#. Mettre les cerises préchargées sur les gâteaux.
#. Mettre les roues dans le plat, à la fin du service.
#. Se déguiser pour faire la fête.
#. Calculer l’addition.

Architecture
************

Choix d'une base holonome à 4 roues de 58mm. 4 roues pour conserver le code de l'année précédente, le développement révélera malheureusement qu'il est nécessaire de revoir le code.
Les différents préhenseur montés sur les élévateurs seront montés dans les espaces vides entre chaque branche de la base holonome.


Robot n°2 POU
=============

- :doc:`/Robot-2023/Tree-ArchiRobot2`

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

Choix d'une toute petite base différentielle, 2 roues à l'arrière, 1 roue folle à l'avant.
Le but de ce robot est de tester la base différentielle et d'en tirer des informations.
