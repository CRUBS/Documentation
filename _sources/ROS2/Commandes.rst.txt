Les exécutables et les launch
=============================

Un exécutable lance un nœud.

.. code-block:: bash
	
	ros2 run nom_paquet nom_executable

Un launch lance plusieurs exécutables.

.. code-block:: bash
	
	ros2 run nom_paquet nom_launch


Les topics
==========

Lister les topics :

.. code-block:: bash

	ros2 topic list

Écouter un topic :

.. code-block:: bash

	ros2 topic echo /nom_du_topic


Infos sur le topic :

.. code-block:: bash

	ros2 topic info /nom_du_topic

Publier sur un topic :

.. code-block:: bash
	
	ros2 topic pub <topic_name> <msg_type> '<args>'

exemple :

.. code-block:: bash

	ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"



Les noeuds
==========

Lister les nœuds :

.. code-block:: bash

	ros2 node list



rqt graph
=========

Permet de visualiser les liens entre les nœuds et les topics sous forme visuelle.

.. code-block:: bash

	ros2 run rqt_graph rqt_graph


rviz
====

rviz permet de visualiser l'environnement détecté par le robot. Par exemple visualiser les données du lidar.

.. code-block:: bash

	rviz2

	



