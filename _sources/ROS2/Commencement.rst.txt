Création d'un workspace
=======================

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
=====================

Afin de séparer les différentes parties d'un projet, il est recommandé de créer plusieurs packages dans le dossier src
de votre espace de travail.

On commence par se rendre dans le dossier source de notre workspace précédemment créé.

.. code-block:: bash

	cd ~/ros2_ws/src

Puis on crée le package.

python
******

.. code-block:: bash

	ros2 pkg create --build-type ament_python my_package


C++
***

.. code-block:: bash

	ros2 pkg create --build-type ament_cmake my_package


Programmes type
===============

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
======================================

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
*****

Pour simplifier la compilation, je recommande de créer un alias pour ne pas à avoir à lancer
les deux lignes précédentes, pour cela, nous allons éditer le fichier *.bashrc* qui gère votre terminal.

.. code-block:: bash

	sudo nano ~/.bashrc

Et y rajouter la ligne suivante à la fin :

.. code-block:: bash

	alias rb='colcon build && source install/setup.sh'

Maintenant en entrant la commande 'rb' dans votre terminal, la compilation puis le sourçage s'effectueront.
