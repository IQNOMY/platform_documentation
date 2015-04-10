.. include:: ../links.rst
.. _api:

##########
How to use
##########

.. contents::

SOAP is not used anymore

REST
====

The REST webservices start with the link: http://management.iqnomy.com/myliquidsuite-ws/rest/dimensions/API

HTTP response format
--------------------
The REST services can response in the formats JSON or XML. The client can set this format by setting a HTTP-header Accept:

for JSON:
Accept: application/json

for XML:
Accept: application/xml

Overview REST services
----------------------

http://liquifier.iqnomy.com/myliquidsuite-ws/api



Authentication of webservices
=============================
Basic authentication is being used.

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

########
Profiles
########

Standard key / values
---------------------

IQNOMY can use a standard set of key values. Based on those key/values standard rules are used. The key values will be connected in the IQNOMY platform in the right way to the user. The values are used also in the [[IQNOMY Magento extension]].

==========================
Ecommerce site integration
==========================

Our IQNOMY script can already track a lot on the website. But to make tracking even better and richer we provide the following layouts:
* Standard webshop layout
* Standard leisure layout
* Custom layout

.. seealso::
   * `IQNOMY Magento extension <magento>`_
   * `SEOshop integration <seoshop>`_
   * `Register event data <events>`_

If you want to know how you can register these standard layouts.

Standard webshop layout
=======================
Every page in the frontend needs to enclose the [[Tracking integration with website|standard IQNOMY script]] just before the closing </body> tag. This standard IQNOMY script will track all the normal pageviews through a Javascript. Next to these page views the following events will be tracked.



    If a visitor registers a new account (account=register)
    If a visitor logs in (account=login)
    If a visitor subscribes for a newsletter (newsletter=true)
    If a visitor posts a contact form (contactform=true)
    If a visitor changes the content of a shopping cart (cart_changed=true, subtotal=<bedrag>, orderrows=[{product_id:<id>,quantity:<aantal>,price:<bedrag>}, ...])
    If a visitor does a checkout of the order (checkout=true)

    If a visitor visits the homepage (page_type=home)
    If a visitor visits a CMS page (page_type=info)
    If a visitor visits a category page (page_type=overview, category_id=<id>)
    If a visitor visits a product detail page (page_type=detail, product_id=<id>, category_id=<id>, <dimension>=<value>, ...)
    If a visitor visits the shopping cart (page_type=shoppingcart)
    If a visitor visits the order page (page_type=checkout)
    If a visitor visits the search result page (page_type=search, search=<zoekterm>)
    If a visitor visits the wish list (page_type=wishlist, products=[{product_id:<id>,category_id:<id>,<dimension>:<value>,...}])
    If a visitor visits the product comparison (page_type=compare, products=[{product_id:<id>,category_id:<id>,<dimension>:<value>,...}])

    If a visitor on product detail page clicks the tab Product properties (details=attributes)
    If a visitor on product detail page clicks the tab Reviews (details=reviews)
    If the filters on a category page are used by a visitor (filter=true, <dimension>=<value>, …)
    If the sorting on the category page is used (order=<dimension>, direction=asc/desc)

Standard leisure layout
=======================

* Campagne
* OrientationPhase
* Vacationperiod
* Location
* Activity
* Composition group
* Funnel
* Funnel fallout
* Adults
* Cottages
* Children
* Animals
* Type accommondation
* Amount bedrooms
* Type visitor
* Type consumer
* Last booking

Custom layout
=============
If you want a custom layout you can contact us at support@iqnomy.com

#########
Event api
#########

request base url: http://liquifier.iqnomy.com/myliquidsuite-ws/rest/trackevent/webshop
request method:  POST

parameters:

+------------+---------+-------------------------------------------------------------------------------------------------------+
|naam        |vereist  |beschrijving                                                                                           |
|tenant      |*ja*     |unieke id van de IQNOMY tenant                                                                         |
|vid         |*ja*     |unieke id van IQNOMY bezoeker waarvan de eventdata verstuurd wordt (clientside bekend onder _iqnomyvid)|
|fid         |*ja*     |gebruikt voor loadbalancing. een willekeurig nummer tussen 0 en 100                                    |
|iqurl       |*ja*     |de url van de pagina waarvan de datavestuurd wordt                                                     |
|externalvid |*ja*     |het alternatieve ID van de IQNOMY bezoeker waarvan de eventdata verstuurd wordt                        |
|canonical   |*nee*    |canonical waaraan de pagina ipv de iqurl herkent moet worden                                           |
|iqversion   |*nee*    | standaard 3                                                                                           |
+------------+---------+-------------------------------------------------------------------------------------------------------+

*POST body*
iqeventdata: *ja*

de eventdata die verstuurd wordt, formatter als application/x-www-form-urlencoded. Elke key-value wordt opgepakt als een eventdata waarde.(gebruik URL encoding op alle niet alpa-numerieke characters) Voorbeeld:

keyvalues:
naam: Jonathan Doe
leeftijd: 23

encoded:
naam=Jonathan+Doe&leeftijd=23

*Voorbeeld:*
.. code-block:: javascript

   http://liquifier.iqnomy.com/myliquidsuite-ws/rest/trackevent/webshop?tenant=763096175&iqversion=3&vid=1383333&fid=1&iqurl=http%3A%2F%2Fdevelop.coww.nl%2F&canonical=http%3A%2F%2Fdevelop.coww.nl%2F

   Headers:	Content-Type: multipart/form-data;
   Body: iqeventdata=checkout%3Dtrue%26kleur%3DRood%26Maat%3DKlein



