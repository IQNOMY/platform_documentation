#########
Mailchimp
#########

.. contents::

Introduction
============

.. include:: ./introliquidemail.rst



Getting started
===============

Mailchimp configuration
=======================

Identification
~~~~~~~~~~~~~~
You will need to put the parameters for email unique id and list unique id into every url of your newsletters. This way IQNOMY will automaticly identify you Mailchimp subscribers.

.. code-block:: javascript

   email : EMAIL = *|EMAIL|* and LIST:UID = *|LIST:UID|*
   euid : EMAIL_UID  = *|EMAIL_UID|* and LIST:UID = *|LIST:UID|*
   email_and_euid: EMAIL = *|EMAIL|* and EMAIL_UID  = *|EMAIL_UID|* and LIST:UID = *|LIST:UID|*

http://www.yourdomain.com/test/mailchimp.html?iqmceuid=4659a68892&iqmcliid=5fbb805b61



MailChimp List requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~

To use IQNOMY in combination with Mailchimp a list must be available. Subscribers can be added and updated to this list. If no list is available yet, you have to create one.

Steps:

#. Login MailChimp
#. Go to top menubar and click **Lists**
#. Click button **Create List**
#. In the grey area click again **Create List**
#. In the opened page fill in the required fields and press **Save**

Now a list is available where IQNOMY can add and update subscribers. Of course you can also use an existing list.

MailChimp List Fields
~~~~~~~~~~~~~~~~~~~~~
Standard a nwe list in Mailchimp has the following fields:
* Email Address (required, can't be removed and is used as unique id)
* First Name (optional, can be removed)
* Last Name (optional, can be removed)

You can add custom fields to the Mailchimp list.

.. note::
   Custom fields are also standard in the Signup Form. Therefor you might want to set the field to *invisible*. See http://kb.mailchimp.com/lists/signup-forms/add-hidden-fields-to-a-signup-form voor meer info.*

Custom Fields can be added throught:

* Signup Forms (editors)
* List fields settings

To set the field invisible

* At Signup Form editor select the custom List field, check **Hidden** and **Save Field**.
* At List field settings overview, go to the row with the custom List field, uncheck **Visible?** and click **Save Changes**

Steps for adding a custom field with the List field settings:

#. Login MailChimp
#. Go to top menubar and click **Lists**
#. Click on the name of the appropriate List
#. Select the List option **Settings** and in the dropdown click **List fields and MERGE tags**
#. Click below **Add a field**
#. Select the type for the custom Field. (TEXT is most of the time the most practical)
#. You can now change the settings
#. Save

.. note::
   Multiple custom fields can be added this way

Mailchimp List Fields -> Naming
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* List fields have a decribing **Field label** and a **Tag**
* The **tag** name is the identifying name of the field
* A field has a **standard tag** name MergeN (N is a number). this is automaticly generated when creating the field.
* Next to the standard tag you can also create a unique Tag
* A tag must be unique within a List

Examples

+------------+----+---------+--------+---------+
|Field label |Type|Required |Visible |Tag      |
+------------+----+---------+--------+---------+
|sessionCount|text|false    |false   |S_COUNT  |
+------------+----+---------+--------+---------+
|pageVisits  |text|false    |false   |PV_COUNT |
+------------+----+---------+--------+---------+
|artikelgroup|text|false    |false   |ART_GROUP|
+------------+----+---------+--------+---------+


API key
~~~~~~~~~~~~~~
General information about the MailChimp REST api can be found at https://apidocs.mailchimp.com/api/2.0/

.. note::
   API keys are connected to a datacenter. The datacenter adres must be in the API url as a subdomain.

.. warning::
   A person that is subscribed through a API call receives and standard acceptionmail from MailChimp. If the person doesn't click the link he will not show up in the list as a subscriber.



