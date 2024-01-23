CIF
===

La CNC CIF  permet de lancer un usinage avec 4 outils différents:
* Fraise javelot hélicoïdale
* Fraise de 2mm
* Forêt 0,9mm et 1,2mm

A l’Ensibs,  cette machine est principalement dédiée au fraisage des circuits imprimés. Le logiciel intégré  Galaad comprend plusieurs modules FAO et s’interface avec le directeur de commande de la CNC.

Module Percival: Préparation de l’usinage
=========================================

Import des fichiers de fabrications
***********************************

* Lancer Percival
* Fichier → ouvrir → nouveau circuit

.. image:: images/cif/Image1.png
	:scale: 100 %
	:align: center

Fixer les chemins des différents répertoires : côtés soudures et composants, perçage.

Détourage de la carte
*********************

Valider le contour  de carte proposé par défaut.

.. image:: images/cif/Image2.png
	:scale: 100 %
	:align: center

Choix du détourage :

* extérieur pour découper la carte
* intérieur pour les trous de fixations

.. image:: images/cif/Image3.png
	:scale: 100 %
	:align: center

Cas d’un PCB simple face
************************

Pour faciliter les manipulations, il est préférable de fermer la couche n° 2 :

* Affiche→ couche n°2
* fichier → fermer la couche

Contours  d'isolations
**********************

* Usinage → Contours d'isolations → Calculer les contours

Si le résultat semble correcte passez à l'opération suivante sinon retoucher le circuit sous :doc:`/CAO/Tree-KiCad`.

Redimensionner
**************

Fichier → Dimension

On reste en recadrage par défaut et ne laissez pas le logiciel modifier la profondeur de perçage.

Transfert vers le module d’usinage fraisage Galaad
**************************************************

.. image:: images/cif/Image4.png
	:scale: 100 %
	:align: center

.. image:: images/cif/Image5.png
	:scale: 100 %
	:align: center

Réglage et préparation de l'usinage sous Galaad
===============================================

Relever la dimension du brut
****************************

Fichier → Dimension du brut


Choisir et coller le brut sur le plateau de la machine
******************************************************

Mesure de planéité
******************

Mettre le palpeur de planéité en place au niveau de la broche et le connecter

.. image:: images/cif/Image6.png
	:scale: 100 %
	:align: center

.. image:: images/cif/Image7.png
	:scale: 100 %
	:align: center

Lancer le relevé de planéité
****************************

	      
* Paramètre→ Machine → complet → avancé
* Décocher/coher   ''Activer la correction de planéité en Z''
* Renseigner les positions sud-ouest et nord-est en fonction de la dimension du brut
* Régler le nombre de relevés de manière à avoir une marge ≤ 20mm

.. image:: images/cif/Image8.png
	:scale: 100 %
	:align: center

Lancer le palpage, récupérer la 1er valeur Za en sud-ouest. Za sera ensuite utilisée pour déterminer l’origine pièce en Z.

.. image:: images/cif/Image9.png
	:scale: 100 %
	:align: center

Accès à l'interface d'usinage  
*****************************

.. image:: images/cif/Image11.png
	:scale: 100 %
	:align: center

Vérifier et si besoin régler la séquence des outils 1-3-4-2

.. image:: images/cif/Image10.png
	:scale: 100 %
	:align: center


* Origine pièce
* Boite de dialogue ''Charger l’outil n°1'' →  OK
* Fixer l’origine pièce X=10, Y=17,  Z=Za-8,25

.. image:: images/cif/Image12.png
	:scale: 100 %
	:align: center

Lancement de l'usinage

.. image:: images/cif/Image13.png
	:scale: 100 %
	:align: center