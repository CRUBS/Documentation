Introduction
============

ROS 2, ou *Robot Operating System 2*, est une plateforme open-source conçue pour faciliter le développement de logiciels
pour les robots. Il s'agit d'une évolution de ROS, offrant une architecture plus modulaire et des améliorations
de performance par rapport à son prédécesseur. ROS 2 a été conçu pour être plus adaptable à un large éventail
de matériels et de systèmes d'exploitation, ce qui en fait une solution polyvalente pour la robotique.
Il offre des outils et des bibliothèques pour la gestion des communications, la gestion des périphériques,
la planification de trajectoires, et bien plus encore, facilitant ainsi le développement de robots et
de systèmes robotiques complexes.

.. image:: images/ros2/ROS_topic.gif
   :scale: 100 %
   :align: center


La distribution ROS2 que nous utilisons est "Humble", dont voici la documentation officielle :
https://docs.ros.org/en/humble/Tutorials.html

Installation et Setup
=====================

.. warning::
    Impératif : ROS2 doit être installé sur une version de l'OS Ubuntu 22.0x, une version antérieure
    telle qu'un Ubuntu 20.0x ne pourra installer ROS2.

Si vous avez déjà une version de ROS ou de ROS2 d'installée sur votre pc nous recommandons de les retirer
pour ne pas rencontrer de problème par la suite.

.. code-block:: bash

	sudo apt-get purge ros-*
	sudo apt-get autoremove

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
	
Lancement de la démo pour vérifier la bonne installation de ROS2.

.. code-block:: bash

	ros2 run demo_nodes_cpp talker

Enfin, on peut supprimer les paquets téléchargés déjà installer puis redémarrer.

.. code-block:: bash

	sudo apt autoremove
	sudo reboot



Bien commencer
==============

Création d'un workspace
***********************

Un workspace, littéralement "espace de travail", est un dossier qui contient vos fichiers source (les packages),
les *install*, les *logs* et les fichiers sources compilés.


.. code-block:: bash

	mkdir -p ~/ros2_ws/src

Vous créez ici le workspace de nom "ros2_ws" (vous pouvez l'appeler comme vous le souhaitez.)
et par la même occasion le dossier *src* qui contiendra les packages.


.. warning::

	Attention votre workspace doit etre créé par l'utilisateur et non le root. Vous pouvez vérifier avec la commande suivante à qui appartient le dossier dans lequel vous vous placez.

.. code-block:: bash

	ll

Vous pouvez, grâce à cette commande, savoir qui est le propriétaire du dossier.

Pour modifier le propriétaire du fichier :

.. code-block:: bash

	sudo chown nom_utilisateur nom_dossier

Maintenant le dossier nous appartient.

Création d'un package
*********************

Afin de séparer les différentes parties d'un projet, il est recommandé de créer plusieurs packages dans le dossier src
de votre espace de travail.

On commence par se rendre dans le dossier source de notre workspace précédemment créé.

.. code-block:: bash

	cd ~/ros2_ws/src

Puis on crée le package.

python
^^^^^^

.. code-block:: bash

	ros2 pkg create --build-type ament_python my_package


C++
^^^

.. code-block:: bash

	ros2 pkg create --build-type ament_cmake my_package


Programmes type
***************

Voici un premier nœud type dans lequel on retrouve tout ce qui est nécessaire pour commencer.

.. code-block:: python

	import rclpy #lib ro2
	from rclpy.node import Node #import de la classe Node
	from std_msgs.msg import String #import du type de message de topic String, cette ligne doit etre adaptée au cas par cas

	#création de notre neoud, ce dernier est un objet herité de la classe Node de la librairie ros2
	class MyNode(Node):
	    def __init__(self):
	        super().__init__('my_node') #nom du noeud en paramètre
	        self.publisher_ = self.create_publisher(String, 'my_topic', 10) #création d'un publisher (type de message, nom du topic, timeout)
	        self.subscription_ = self.create_subscription(String, 'my_topic', self.callback, 10) #création d'un subscriber (type de message, nom du topic, fonction à appeler, timeout)
	        self.timer_ = self.create_timer(1.0, self.timer_callback) #création d'un timer (période, fonction à appeler)
	        self.get_logger().info('Node initialized')

	    def callback(self, msg):
	    	#cette fonction est appelée à chaque fois qu'un message est lu
	        self.get_logger().info('Received message: "%s"' % msg.data) #renvoie le message lu

	    def timer_callback(self):
	    	# cette fonction est appelée à une certaine fréquence définie à la création du timer
	        msg = String() #création de l'objet msg
	        msg.data = 'Hello, ROS 2!' #on remplit le message
	        self.publisher_.publish(msg) #on publie sur le publisher
	        self.get_logger().info('Published message: "%s"' % msg.data)

	#en dessous les lignes suivantes sont obligatoire et toujours en fin de programme
	#création de la fonction main
	def main(args=None):
	    rclpy.init(args=args)
	    node = MyNode()
	    rclpy.spin(node)
	    rclpy.shutdown()

	if __name__ == '__main__':
	    main()


Compilation d'un workspace avec colcon
**************************************

À chaque fois qu'un fichier est modifié, il est nécessaire de compiler de nouveau votre espace de travail.
Pour cela, placez-vous dans votre workspace puis entrez la commande suivante.

Commencez par vous placer dans votre workspace :

.. code-block:: bash

	cd ~/ros2_ws

Puis vous pouvez compiler.

.. code-block:: bash

	colcon build

Vous pouvez aussi compiler un package en particulier pour gagner du temps

.. code-block:: bash

	colcon build --packages-select my_package

Une fois la compilation terminée, il est nécessaire de sourcer de nouveau votre travail.
La compilation a créé le fichier bash (.sh) nécessaire à l'installation.

.. code-block:: bash

	source install/setup.sh

Alias
^^^^^

Pour simplifier la compilation, je recommande de créer un alias pour ne pas à avoir à lancer
les deux lignes précédentes, pour cela, nous allons éditer le fichier *.bashrc* qui gère votre terminal.

.. code-block:: bash

	sudo nano ~/.bashrc

Et y rajouter la ligne suivante à la fin :

.. code-block:: bash

	alias rb='colcon build && source install/setup.sh'

Maintenant en entrant la commande 'rb' dans votre terminal, la compilation puis le sourçage s'effectueront.


Configuration des exécutables
=============================

Python
******

Lors de la création d'un package un fichier setup.py est automatiquement créé.
Ce fichier permet de paramétrer les executable. Cette étape est importante afin d'exécuter vos scripts.

Vous devez rajouter la ligne suivante dans la liste 'console_scripts' à la fin du fichier :

.. code-block:: bash

	'my_script = my_package.my_script:main'

Ce qui signifie :

.. code-block:: text

	nom_de_l_executable = nom_du_package.nom_du_script:main

Attention a bien suivre la structure du nœud présenté ci-dessus.

Vous pouvez en ajouter plusieurs tel que :

.. code-block:: bash

	from setuptools import setup

	package_name = 'my_package'

	setup(
	    name=package_name,
	    version='0.0.0',
	    packages=[package_name],
	    data_files=[
	        ('share/ament_index/resource_index/packages',
	            ['resource/' + package_name]),
	        ('share/' + package_name, ['package.xml']),
	    ],
	    install_requires=['setuptools'],
	    zip_safe=True,
	    maintainer='ubuntu',
	    maintainer_email='ubuntu@todo.todo',
	    description='TODO: Package description',
	    license='TODO: License declaration',
	    tests_require=['pytest'],
	    entry_points={
	        'console_scripts': [
	        	'exec_1 = my_package.script_1:main',
	        	'exec_2 = my_package.script_2:main'
	        ],
	    },
	)

Ici nous avons ajouté les exécutables exec_1 et exec_2 qui appellent les fonctions *main* de *script_1* et *script_2*.

C++
***

na


Configuration des Launch
========================


Avant de créer vos fichiers *launch* vous devez créer un dossier spécifique dans votre package si ce dernier n'existe pas.

.. code-block:: bash

	mkdir launch

Python
******

Voici maintenant un exemple de fichier *launch*. Ici ce dernier lance 3 executables. Beaucoup de paramètres peuvent être ajoutés.


.. code-block:: python

	from launch import LaunchDescription
	from launch_ros.actions import Node

	def generate_launch_description():
	    return LaunchDescription([
	        Node(
	            package='nom_du_package_de_lexecutable',
	            executable='nom_de_lexecutable_a_lancer',
	            name='nom_pour_vous_y_retrouver_vous_pouvez_remettre_le_nom_de_lexecutable'
	        ),
	        Node(
	            package='turtlesim',
	            executable='turtlesim_node',
	            name='sim'
	        ),
	        Node(
	            package='turtlesim',
	            executable='mimic',
	            name='mimic',
	            remappings=[
	                ('/input/pose', '/turtlesim1/turtle1/pose'),
	                ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
	            ]
	        )
	    ])

Un launch file peut lancer des exécutables present dans un autre package que celui où se trouve votre launch file.

Commandes importantes
=====================

Les exécutables
***************

Un exécutable lance un nœud.

.. code-block:: bash
	
	ros2 run nom_paquet nom_executable


Les launchs
***********

Un launch lance plusieurs exécutables.

.. code-block:: bash
	
	ros2 run nom_paquet nom_launch


Les topics
**********

Lister les topics :

.. code-block:: bash

	ros2 topic list

Écouter un topic :

.. code-block:: bash

	ros2 topic echo /nom_du_topic


Infos sur le topic :

.. code-block:: bash

	ros2 topic info /nom_du_topic


Les noeuds
**********

Lister les nœuds :

.. code-block:: bash

	ros2 node list



rqt graph
*********

Permet de visualiser les liens entre les nœuds et les topics sous forme visuelle.

.. code-block:: bash

	ros2 run rqt_graph rqt_graph


rviz
****

rviz permet de visualiser l'environnement détecté par le robot. Par exemple visualiser les données du lidar.

.. code-block:: bash

	rviz2

	



