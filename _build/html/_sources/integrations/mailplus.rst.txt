.. include:: ../links.rst

.. _Mailplus:

########
MailPlus
########

Introduction
============

.. include:: ./introliquidemail.rst

Getting started
===============
MailPlus configuration
~~~~~~~~~~~~~~~~~~~~~~
Custom fields should be created in MailPlus to use the IQNOMY integration. In those custom fields IQNOMY will store extra data.

When you open the List Manager of MailPlus the first tab 'Overview targetgroups' will automaticly open. All your contacts are available here. Your email contacts are devided in groups. The group everybody contains all contacts.

The MailPlus contactperson structure is the same within your account. If you create extra custom fields they will be available for every contact person in your account. There is a limit in creating custom fields. http://kennis.mailplus.nl/module/list-manager/profielvelden-bewerken/?user-type=ecom&lang=nl

Add custom fields
~~~~~~~~~~~~~~~~~
* Go to listmanager
* Select tab Edit Profile fields
* For every custom field -> choose profile x (x = number) -> toggle visible (on/off) -> choose custom label

Send IQNOMY the following info
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Tenant id (liquid account id): from the IQNOMY platform. :ref:`liquid-account-details`
* Consumer key: This is the MailPlus "API key". `MailPlus REST API information`_
* Consumer secret: This is the MailPlus "API Secret". `MailPlus REST API information`_
* Name custom contact field: The MailPlus contact field where IQNOMY can store profile data. Example: *IQNOMY - Referrer {profiel4}*

Send this info to `Contact us`_



Identification
~~~~~~~~~~~~~~
The identification of IQNOMY and MailPlus should connect in order to recognize website visitors as MailPlus contacts. Every link in a newsletter subscribers receive, needs to contain the MailPlus id. If a subscriber clicks a link the webpage will open and IQNOMY recognizes the id from the link. You must use the parameter *iqmpid*.

You will need to use the *{externKlantId}*. When sending the newsletter this will be replaced by an unique subscriber id.

* http://www.yourdomain.com/?iqmpid={externKlantId}

Examples:
* http://www.yourdomain.com/?iqmpid=12313248234
* http://www.yourdomain.com/index.php?utm_medium=email&iqmpid=12383463

