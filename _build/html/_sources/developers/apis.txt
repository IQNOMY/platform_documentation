.. include:: ../links.rst

   
###
API
###

.. contents::

.. _apidoc:

REST
====

HTTP response format
--------------------

The REST services can response in the formats JSON or XML. The client can set this format by setting a HTTP-header Accept:

for JSON:
    Accept: application/json
for XML:
    Accept: application/xml

Overview REST services
----------------------

The REST webservices start with the link: http://liquifier.iqnomy.com/myliquidsuite-ws/api/

Authentication of webservices
=============================

Basic authentication is being used.

.. warning:: We are working on OAUTH2. This is expected to be live at the end of 2015. 

Username: ''Username''*''Account''

.. note::
 Example: christian@iqnomy.com*15854915

Webservice key: This is a random generated key. You can find this key in IQNOMY > Discovery > integration on own website

.. note::
 Example: 65565245664b7063357a533157356a6966546c494e77433645635a594878527a496f38663037554a

* Username: the emailadres you use to login to IQNOMY.
* Account: User the IQNOMY id of your environment Example 763096175
* Webservice key: API key

You can find your IQNOMY ID and Webservice key in your IQNOMY account in Discovery > Connect IQNOMY

If your infrastructure requires other security protocols please contact support@iqnomy.com

.. _eventapi:

#########
Event api
#########

.. seealso::
  :ref:`events`

* request base url: http://liquifier.iqnomy.com/myliquidsuite-ws/rest/trackevent/webshop
* request method:  POST

parameters:

+------------+---------+-------------------------------------------------------------------------------------------------------+
|naam        |vereist  |beschrijving                                                                                           |
+------------+---------+-------------------------------------------------------------------------------------------------------+
|tenant      |*ja*     |unieke id van de IQNOMY tenant                                                                         |
+------------+---------+-------------------------------------------------------------------------------------------------------+
|vid         |*ja*     |unieke id van IQNOMY bezoeker waarvan de eventdata verstuurd wordt (clientside bekend onder _iqnomyvid)|
+------------+---------+-------------------------------------------------------------------------------------------------------+
|fid         |*ja*     |gebruikt voor loadbalancing. een willekeurig nummer tussen 0 en 100                                    |
+------------+---------+-------------------------------------------------------------------------------------------------------+
|iqurl       |*ja*     |de url van de pagina waarvan de datavestuurd wordt                                                     |
+------------+---------+-------------------------------------------------------------------------------------------------------+
|externalvid |*ja*     |het alternatieve ID van de IQNOMY bezoeker waarvan de eventdata verstuurd wordt                        |
+------------+---------+-------------------------------------------------------------------------------------------------------+
|canonical   |*nee*    |canonical waaraan de pagina ipv de iqurl herkent moet worden                                           |
+------------+---------+-------------------------------------------------------------------------------------------------------+
|iqversion   |*nee*    | standaard 3                                                                                           |
+------------+---------+-------------------------------------------------------------------------------------------------------+

| POST body
| iqeventdata: ja

De eventdata die verstuurd wordt, formatter als application/x-www-form-urlencoded. Elke key-value wordt opgepakt als een eventdata waarde.(gebruik URL encoding op alle niet alpa-numerieke characters) Voorbeeld:

| keyvalues:
| naam: Jonathan Doe
| leeftijd: 23
|
| encoded:
| naam=Jonathan+Doe&leeftijd=23


*Voorbeeld:*

.. code-block:: javascript

   http://liquifier.iqnomy.com/myliquidsuite-ws/rest/trackevent/webshop?tenant=763096175&iqversion=3&vid=1383333&fid=1&iqurl=http%3A%2F%2Fdevelop.coww.nl%2F&canonical=http%3A%2F%2Fdevelop.coww.nl%2F

   Headers:	Content-Type: multipart/form-data;
   Body: iqeventdata=checkout%3Dtrue%26kleur%3DRood%26Maat%3DKlein



