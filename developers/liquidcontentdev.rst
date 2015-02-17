##############
Liquid content
##############

Het is mogelijk om custom javascript-code toe te voegen aan een liquid content. Deze code wordt uitgevoerd op het moment dat de liquid content getoond wordt.
 
In de template van de liquid content dien je je custom javascript-code te plaatsen in een script-tag geïdentificeerd met "_iqnomy_extrascript". Voorbeeld:

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
     alert('custom code');
   </script>
 
Hieronder verschillende manieren om dit te implementeren.
 
Toepassing 1
============
 
- minder goed onderhoudbaar als custom script in meerdere liquid contents nodig is
- geen aanpassing aan container-pagina's nodig
 
In liquid content plaatsen:

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
     alert('custom code');
   </script>
 
Toepassing 2a:
==============
 
- beter onderhoudbaar als custom script in meerdere liquid contents nodig is
- wel aanpassing aan container-pagina's nodig
- minder goed onderhoudbaar als custom script op meerdere pagina's nodig is.
 
In liquid content plaatsen:

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
   myFunction('custom code');
   </script>
 
In container-pagina plaatsen:

.. code-block:: javascript

   <script type="text/javascript">
     function myFunction(str) {
       alert(str);
     }
   </script>
 
 
Toepassing 2b:
==============
 
- beter onderhoudbaar als custom script in meerdere liquid contents nodig is
- wel aanpassing aan container-pagina's nodig
- beter onderhoudbaar als custom script op meerdere pagina's nodig is
- javascript include-bestand dient beschikbaar te zijn op de website

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
     myFunction('custom code');
   </script>
 
In container-pagina plaatsen:

.. code-block:: javascript

   <script type="text/javascript" src="/my-include.js">
   </script>
 
In /my-include.js plaatsen:

.. code-block:: javascript

   function myFunction(str) {
     alert(str);
   }


*********************
Layout liquid content
*********************

Using standard layouts
======================

A liquid content can be presented in any way you like. If your CMS does the presentation the liquid content will 'advise' your CMS to present eg. id 1300.

You can also use the HTML template to present the Liquid content. In this HTML template you can use different code's to reuse the liquid content data

* $liquidContentUrl : the link URL will be used.
* $impressionUrlParam : the platform will add an unique lqiid (liquid id) to the URL. This way the MLS can track a click on the link.
* $liquidContentName : the title of the liquid content is used.
* $liquidContentDescription : the liquid content description is used.
* $containerSelectorType$escalationCause: This will show the way the liquid content was selected. You can use this variable to track this in analytics tools.

If you want to use javascript in your html template.


