Introduction
============

Les Raspberry Pi sont des "mini ordinateur". Ces dernier peuvent recevoir different OS d'une declinaison linux telle que `Ubuntu 22.04 <https://releases.ubuntu.com/jammy/>` que nous utilisons pour les robots. Une distribution plus legere est RaspiOS aussi appeler Raspbian.

- :doc:`/Informatique_Programmation/Tree-Ubuntu`
- :doc:`/Informatique_Programmation/Tree-Raspbian`



Demarage
========

Installation
************
 
Afin d'installer un os sur une la carte SD vous pouvez utiliser `Raspberry Pi Imager <https://www.raspberrypi.com/software/>`_ qui est un logiciel vous permettant de selectionner l'OS de votre choix

.. image:: images/raspi/raspi_imager.png
	:scale: 75 %
	:align: center


Mises à jours
*************

Je recommande d'utiliser l'interface graphqiue pour ces premieres etapes.


commencons par mettre a jour la pi

.. code-block:: bash
	
	cd
	sudo apt update
	sudo apt-get update
	sudo apt upgrade
	sudo apt-get upgrade

ensuite il va falloir installer le service de ssh

.. code-block:: bash

	sudo apt-get install openssh-client
	sudo apt-get install openssh-server
	sudo systemctl enable ssh
	sudo systemctl start ssh
	sudo systemctl status ssh

verifions que le service ssh c'est bien installer, vous devriez le voir actif comme ci dessous

.. image:: images/raspi/ssh_systemctl.png
   :scale: 75 %
   :align: center




