.. index:: Copernica
.. _Copernica:

.. include:: ../links.rst

#########
Copernica
#########

.. contents::

Introduction
============
It becomes more and more important to know what your customers want. IQNOMY will help you achieving this. As a technology partner we developed together with Copernica a personalization plugin.

.. include:: ./introliquidemail.rst

.. _copernica_configuration:

Getting started
===============
You will need to have a Copernica and IQNOMY account.

#. Create Copernica API key for connection
#. Send API key and database id to IQNOMY consultant.
#. Send the exact names of the database fields for the data you need from IQNOMY. IQNOMY will be configured.
#. Send newsletters with Copernica id in the URL

Now IQNOMY will recognize your subscribers on the website.


Copernica configuration
=======================
Identification
~~~~~~~~~~~~~~
Put the Copernica id in the links of all your newsletters with the prefix iqcopid.

To put the id in a link you can use the Copernica placement {$id}. IQNOMY will recognize the **iqcopid** parameter automaticly when it is used in an URL.
So you have to use *iqcopid={$id}* in all the URL's that go to your website in your newsletter.

*examples*

* http://www.yourdomain.com/?iqcopid=12313248234
* http://www.yourdomain.com/index.php?utm_medium=email&iqcopid=12383463

.. warning::
   Within every Copernica database a customer has a different Copernica ID. So emailadres is not a Copernica id.

API key, database, database fields
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Copernica api key
+++++++++++++++++
You can request a token in your `Copernica application dashboard <https://www.copernica.com/en/applications>`_.

Database id
+++++++++++
In Copernica you can have several databases. We need to know which database we need to update. You can find your database id if you hover with your mouse over the database. It will popup as a mousetip.

Database fields
+++++++++++++++
Based on the information from the website you want to store, IQNOMY will update these fields. Copernica will need those field predefined. So if you want to store a field with the subscribers interest. You will need to create the databasefield **interest** and send this fieldname to the IQNOMY consultant. He will configure IQNQMY to store the profile information in this database field in Copernica.

.. seealso::
   * `Liquid email marketing cases`_
   * `Introductie in liquid email marketing`_
   * `Ook alle IQNOMY informatie in jou systemen`_

Example case
================
This IQNOMY customer has integrated IQNOMY with their Copernica account.

Their **goal**: Send personal emails based on the website visit

What is the case
----------------

#. All customers get a newsletter: The links have Copernica id's
#. Customers click on the link: Now we can recognize a Copernica visitor on the website
#. Customer searches on the website: All data is send to IQNOMY
#. At the end of a visit IQNOMY sends the info to Copernica
#. Based on the data and marketing goals Copernica will send an email

.. figure:: _static/images/WebsiteHolidayCars.png
   :scale: 50 %
   :alt: Visitor searches on website

.. figure:: _static/images/Holidaycars.png

.. image:: _static/images/Holidaycars2.png

.. image:: _static/images/SearchDate.png

How to implement this case
--------------------------
#. You need an :doc:`IQNOMY <../starthere/gettingstarted>` and Copernica account
#. :ref:`Configure the Copernica <copernica_configuration>` newsletters and database
#. IQNOMY will configure the integration
#. Test your new integration
#. Send your customers personalized emails



