Préparation
===========

.. danger::
    Impératif : ROS2 doit être installé sur une version de l'OS Ubuntu 22.0x, une version antérieure
    telle qu'un Ubuntu 20.0x ne pourra installer ROS2.

Si vous avez déjà une version de ROS ou de ROS2 d'installée sur votre pc nous recommandons de les retirer
pour ne pas rencontrer de problème par la suite.

.. code-block:: bash

	sudo apt-get purge ros-*
	sudo apt-get autoremove

Installation
============

Voici désormais les étapes pour l'installation de ROS2 Humble. Ces étapes sont valides pour un PC
comme pour une Raspberry Pi du moment que le système d'exploitation est Ubuntu.

.. note::

	Attention il est possible que cette démarche d'installation ne fonctionne plus, à ce moment veuillez vous référer à la documentation de ROS2 et mettez à jour cette documentation : https://docs.ros.org/en/humble/Installation/Alternatives/Ubuntu-Development-Setup.html

Commençons par mettre à jour le gestionnaire de paquets de l'ordinateur.

.. code-block:: bash
	
	cd
	sudo apt update
	sudo apt-get update
	sudo apt upgrade
	sudo apt-get upgrade

Vérifions que la configuration en utf-8 est bien en anglais américain.

.. code-block:: bash

	locale  # check for UTF-8

	sudo apt update && sudo apt install locales
	sudo locale-gen en_US en_US.UTF-8
	sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
	export LANG=en_US.UTF-8

	locale  # verify settings

Téléchargement des dépôts ROS2.

.. code-block:: bash


	sudo apt install software-properties-common
	sudo add-apt-repository universe

	sudo apt update && sudo apt install curl -y
	sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg


	# Ajout du dépôt à la liste des paquets
	echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

	sudo apt update
	sudo apt upgrade

Installation de ROS2 et de ces composantes de navigation, cela peut prendre un bon moment.

.. code-block:: bash

	sudo apt install ros-humble-desktop
	sudo apt install ros-humble-ros-base
	sudo apt install ros-dev-tools

	echo "source /opt/ros/humble/setup.bash" >> .bashrc 

	source .bashrc

	sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup ros-humble-turtlebot3*

Installation et sourçage des variables d'environnement de service dds pour la communication à distance.
Cela peut être très long. Une fenêtre vous demandant d'accepter la licence RTI qui s'ouvrira pendant l'installation,
vous devez accepter. Cette étape n'est pas obligatoire au fonctionnement de ROS2.

.. code-block:: bash

	sudo apt install -q -y rti-connext-dds-6.0.1

	cd /opt/rti.com/rti_connext_dds-6.0.1/resource/scripts && source ./rtisetenv_x64Linux4gcc7.3.0.bash; cd -

Installation de *colcon* pour compiler les packages.

.. code-block:: bash

	sudo apt install python3-colcon-common-extensions

Finalisation
============

Lancement de la démo pour vérifier la bonne installation de ROS2.

.. code-block:: bash

	ros2 run demo_nodes_cpp talker

Enfin, on peut supprimer les paquets téléchargés déjà installer puis redémarrer.

.. code-block:: bash

	sudo apt autoremove
	sudo reboot
