Introduction
============

Cette documentation a ete commencer en 2022. L'objectif est de garder une trace du travail realiser par les membres du CRUBS entre 2021 et 2024. c'est 3 année ont ete fructueuse avec un retour a la coupe de france de robotique et il serait dommage de perdre tout le travail realiser. Cette page a donc pour but de permettre une reprise de cette documentation pour continuer le travail. Cette docuemtation est creer dans un language que l'on appel le RestructuredText.


la `documentation sphinx <https://www.sphinx-doc.org/en/master/>`_ est disponible en ligne et sera utile en cas de besoin

Info supplementaire sur la syntax du restructuredText : https://sublime-and-sphinx-guide.readthedocs.io/en/latest/lists.html


Commencement
============

Generation
**********

Ordonancement des fichiers et des dossiers
******************************************

index
*****

compilation
***********

Generalités
===========

Titres
******

.. code-block:: rst

	ceci est texte

	ici un titre principale
	=======================

	maintenant un titre secondaire
	******************************

	et enfin un titre teriaire
	^^^^^^^^^^^^^^^^^^^^^^^^^^

Format de texte
***************

.. code-block:: rst

	texte en *italique*

texte en *italique*

.. code-block:: rst

	texte en **gras**

texte en **italique**


Liste et enumeration
********************

liste numerauté

.. code-block:: rst

	#. point 1
	#. point 2
	#. point 3

#. point 1
#. point 2
#. point 3

liste a point

.. code-block:: rst

	* point 1
	* point 2
	* point 3

* point 1
* point 2
* point 3

tableaux
********

notes
*****

.. code-block:: rst
	
	.. note::
		ceci est une note

.. note::
	ceci est une note


warnings
********

.. code-block:: rst

	.. warning::
		ceci est un warning

.. warning::
	ceci est un warning



Ajout de media
==============

Attention les syntaxe sont a respecter imperativement, les tabulation, saut de ligne, espace, etc ...

block de code
*************

Exemple d'un block de code a ajouter a la page, vous pouvez evidement remplacer "pyhton" par le language que vous utiliser. 

.. code-block:: rst

	.. code-block:: python

		import math

		def main():
			print("Hello World !")

		if __name__ == "__main__":
			main()

images
******

.. code-block:: rst

	.. image:: chemin/de/limage.png
	   :scale: 20 %
	   :align: center
	   :class: with_shadow float_right

ici l'image est rescale a 20% de sa taille originale, elle est aligner au centre de la page horizontalement. La ligne class, permet de la placer a droite de la page sans faire descendre le texte ce que j'utilise pour les toctree de chaque sujet

beaucoup de parametre existe dans la doc


hyperlien
*********

.. code-block:: rst

	`exemple de lien <page_web.html>`_


lien documentation
******************

.. code-block:: rst

	- :doc:`/Chemin/dans/la/doc`


Herberger la documentation sur github
=====================================

























