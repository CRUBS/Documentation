Introduction
============

Afin de permetre aux robots de reperer leur environnement et principalement les robots adversaires, plusieur solutions existent. Apres avoir observer des resultats trop imprecis avec les prototypes des balises, nous avons du nous rabattratre sur la solution la plus couteuse qui est l'achat de deux lidar. Nous avons selectionner les LD06, ces derniers sont deja utiliser dans le domaine de la robotique et par des equipes de la coupe de france ainsi tous les packages ROS2 existent pour ce dernier

Cablage
=======

Un module de conversion ttl vers serie est necessaire afin de connecter le lidar a la pi en USB (ref : CP2102). voici le cablage :

#. lidar pin 1 : blanc : tx -> module ttl : rx
#. lidar pin 2 : jaune : pwm -> N/A
#. lidar pin 3 : rouge : gnd -> module ttl : gnd
#. lidar pin 4 : bleu : 5v -> module ttl : 5v

Installation
============

tuto video suivis : https://www.youtube.com/watch?v=OJWAsV6-0GE

creation d'un workspace avant de telecharger les paquets:

.. code-block:: bash

	mkdir -p ldlidar_ros2_ws/src
	cd ldlidar_ros2_ws/src

puis copie d'un repertoire git

.. code-block:: bash

	git clone https://github.com/ldrobotSensorTeam/ldlidar_stl_ros2.git
	cd ~

vous pouvez desormais brancher le lidar et verfier avec la commande suivante le nom de son ports USB

.. code-block:: bash

	ls /dev/ttyUSB*

.. image:: images/lidar/port_name.png
   :scale: 100 %
   :align: center

noter bien le numero du port USB, dans mon cas /dev/ttyUSB0
ajoutons lui les droits 

.. code-block:: bash

	sudo chmod 777 /dev/ttyUSB0

nous allons maintenant modifier le fichier de launch du lidar afin de lui indiquer le ports sur lequel ce dernier est connecter

.. code-block:: bash

	cd ~
	cd ldlidar_ros2_ws/src/ldlidar_stl_ros2/launch
	nano ld06.launch.py

maintenant trouvez la ligne suivante et modifier la en fonction de votre ports USB utiliser par le lidar, dans mon cas le /dev/ttyUSB0  est deja indiquer par defaut a la ligne 45

.. code-block:: python

	'port_name': '/dev/ttyUSB0'

.. image:: images/lidar/launch_file.png
   :scale: 100 %
   :align: center

une fois la modification effectuer pour pouvez fermer et enregistrer le fichier avec ctrl+x puis y

a l'avanir le nom du port usb utiliser sera fixer en tant que '/dev/Lidar_LD06' (se referer au tuto dans la configuration Ubuntu). 

Lancement du lidar
==================

Maintenant que le package du lidar est correctement configurer, nous allons pouvoir le faire fonctionner afin de visualiser notre environnemment

Nous devons build le package puis sourcer les variables d'environnement

.. code-block:: bash

	cd ~
	cd ldlidar_ros2_ws
	colcon build
	source install/setup.sh
	source ~/.bashrc

nous pouvons enfin lancer le noeud du lidar

.. code-block:: bash

	ros2 launch ldlidar_stl_ros2 ld06.launch.py

dans un nouveau terminal vous pouvez verifier que le topic /scan est bien present

.. code-block:: bash

	ros2 topic list

Visualisation du lidar
======================

lancer le lidar comme vu au dessus puis lancement de rviz

.. code-block:: bash

	rviz2

en bas a gauche de la fenetre cliquer sur Add puis dans le volets qui viens de s'ouvrir choisir LaserScan et Ok

vous allez maintenant devoir selectionner plusieurs parametre du menu de gauche

#. dans Global Options > Fixed Frame choisir base_link
#. dans LaserScan > Topic choisir /scan

des points de couleurs de couleur devrais apparaitre dans l'interface centrale de rviz representant les resultats du lidar





