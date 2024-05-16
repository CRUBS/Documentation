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
