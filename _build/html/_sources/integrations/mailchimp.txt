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

\\
Standaard waren de volgende velden al aanwezig:
|Field label|Type|Required|Visible|Tag|
|Email Address|email|always|always|EMAIL|
|First Name|text|false|always|FNAME|
|Last Name|text|false|always|LNAME|

**************
Stap 2 Api key
**************

Stap 2
* Opschrijven met welke api aanroepen de volgende acties uitgevoerd kunnen worden. Per actie moet
api aanroep en de bijbehorende parameters en responses opgeschreven worden.
** Token aanmaken
** Controleren of profiel bestaat
** Profiel ophalen
** Profiel aanmaken
** Profiel updaten
* Deze aanroepen testen met advanced restclient


*Algemene info over MailChimp REST api*
https://apidocs.mailchimp.com/api/2.0/

*Let erop!: API Keys zijn gekoppeld aan een vast datacentrum. Het datacentrum adres moet in de API url als subdomein worden toegevoegd. Wanneer een API key gebruikt wordt die niet matched met het datacentrum zal de API aanroep mislukken! Zie eerste deel API Endpoint MailChimp REST info*
\\
|API Key|8e9f9a5c34667ef2aa9dc25de63d956a4-us8|
|datacentrum|us8|
|voorbeeld url|https://us1.api.mailchimp.com/2.0/lists/list.json|
|resultaat|*mislukt*|
|response|{code}
{
    "status": "error",
    "code": 104,
    "name": "Invalid_ApiKey",
    "error": "Invalid MailChimp API Key: 8e9f9a5c4667ef2aa9dc25de63d956a4"
}
{code}|
\\
|API Key|8e9f9a5c34667ef2aa9dc25de63d956a4-us8|
|datacentrum|us8|
|voorbeeld url|https://us8.api.mailchimp.com/2.0/lists/list.json|
|resultaat|*succes*|
\\

*MailChimp OAuth 2.0*
MailChimp maakt voor het gebruik van OAuth 2.0, als authenticatie voor de REST API.

(https://apidocs.mailchimp.com/oauth2/)

*Profiel aanmaken* https://apidocs.mailchimp.com/api/2.0/lists/subscribe.php

Ter info:

* *Wanneer iemand gesubscribed wordt aan de hand van deze API call krijgt de ingeschreven persoon standaard een bevestigingsmail, met een bevestigingslink. Wanneer de persoon niet klikt op deze link zal hij niet toegevoegd worden aan de List. Dit kan met een parameter uitgezet worden echter kan MailChimp het account suspenden wanneer dit misbruikt wordt. (Niet aangeraden dus)*
* *Wanneer een bestaande subscriber wordt toegevoegd en de update parameter wordt meegegeven wordt de subscriber geupdatet*


************
Stap 3
***********
*New Test instructions:*

1 - Create a MailChimp campaign with a template that has a link with:
* iqmcmail or/and iqmceuid queryparam
* iqmcliid queryparam

You can add them by using the following merge_vars tags combined with the queryparam
|iqmcmail=\*\|EMAIL\|\*|email of the user|
|iqmceuid=\*\|EMAIL_UID\|\* |unique id of the user|
|iqmcliid=\*\|LIST:UID\|\* |unique id of the list the campaign is send from|

*Example:*
{code}
http://www.christianvriens.com/test/mailchimp.html?iqmcmail=*|EMAIL|*&iqmceuid=*|EMAIL_UID|*&iqmcliid=*|LIST:UID|*
{code}

h3. 2 - Enable dimension "Visitors connected with MailChimp"

h3. 3 - Add eventrule for saving visitor basic info (firstname,lastname) when they are added to the eventdata (from queryparams or explicitly by eventparams)
When firstname or lastname is added as a queryparam with a specific value, the values are also updated in MailChimp.
*See step 5.1*

{code}
// service.enableLog();
// service.log("Event - Custom - Event - Custom - Update Visitor basicinfo");
//
// Event - Custom - Event - Custom - Update Visitor basicinfo
//
// Save
// none
//
// Use
// none
//
// Relation

var logPrefix = "Event - Custom - Event - Custom - Update Visitor basicinfo - ";

var email = service.getEventProperty('email');
var firstname = service.getEventProperty('firstname');
var lastname = service.getEventProperty('lastname');

if(!StringHelper.isEmpty(email)){
	service.setVisitorProperty("iqVisitorEmail",email);
}
if(!StringHelper.isEmpty(firstname)){
	service.setVisitorProperty("iqVisitorFirstName",firstname);
}
if(!StringHelper.isEmpty(lastname)){
	service.setVisitorProperty("iqVisitorLastName",lastname);
}
return null;
{code}

h3. 4 - Add dimensionrule for updating MailChimp contact with IQNOMY info.
Before saving the rule, replace $\{testdimensionid1\} and $\{testdimensionid2\} with a id (e.g. 1234l -> l for long) of a dimension of the tenant the rule is added to!


h3. 5 - Click the on the link send by the MailChimp campaign to go to the tenants page and to connect the visitor as MailChimp within IQNOMY

h3. 5.1 - (Optional) Generate a pagevisit with the queryparams firstname or lastname to set the visitors firstname and/or lastname

e.g. If the tenants website is www.tenantwebsite.nl -> go to the url www.tenantwebsite.nl\?firstname=test1&lastname=test2 in your browser
You can change the test1 and test2 to any value you like

.. image:: _static/images/Mailchimp_create_list.png
.. image:: _static/images/Mailchimp_embedded_form.png
