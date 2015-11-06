#######
Profile
#######

.. contents::

**********
Profile id
**********

.. glossary::
   Profile
     The profile is based on a unique identification together with properties and connected eventproperties that can be grouped by an session

Connect your id with the IQNOMY profile
=======================================

If you want to recognize a visitors profile based on your id. You can connect your id with the iqnomy profile. This way you can use your id to identify the visitor.

It works two ways:

* IQNOMY can use the information you have with your id in the IQNOMY profile. 
* Based on your ID you can extract information from the IQNOMY platform.

Examples for your ID can be:

* emailid from the emailmarketing system
* your CRM id
* the login id from your website

###################
Add data to profile
###################

You can add information into the IQNOMY profile of your visitor.

Examples can be:

* Extra information from your CRM
* Emailmarketing information
* SEA information
* SEO information

If you send an emailmarketing newsletter, put extra information into the links of you newsletter. This can be an example of the productcategory, age of the receiver, name of the receiver, etc. Example: http://www.iqnomy.com/blog/?name=christian. In this example the IQNOMY profile now knows the name of the visitor.

.. _events:

*******************************
Event data for profile building
*******************************

Connect data with a profile
===========================

Input of data into a profile can be used from all connected channels.

Example
-------

* CRM information
* Information about from campaigns
* Other identifiers
* Form input
* Profiles from other applications
* etc.

Make sure that the things you do are legal looking at privacy of your anonymous visitor. It's your responsibility that the visitors privacy is being respected. We can disconnect IQNOMY if we suspect any legal rights are being violated.

Methods to register data
========================

An event is used to register data with a profile:

#. Page-load: :ref:`websitescript <scripteventdata>`
#. TrackEvent: :ref:`websitescript <scripteventdata>`
#. URL parameters: :ref:`websitescript <scripteventdata>`
#. Using :ref:`REST to register data <eventapi>` 

.. seealso::
  Integrate with REST :ref:`eventapi` or with the :ref:`websitescript <scripteventdata>`

Standard key / values
=====================

IQNOMY can use a standard set of key values. Based on those key/values standard rules are used. The key values will be connected in the IQNOMY platform in the right way to the user.

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

Every page in the frontend needs to enclose the :ref:`websitescript` just before the closing </body> tag. This standard IQNOMY script will track all the normal pageviews through a Javascript. Next to these page views the following events will be tracked.



* If a visitor registers a new account (account=register)
* If a visitor logs in (account=login)
* If a visitor subscribes for a newsletter (newsletter=true)
* If a visitor posts a contact form (contactform=true)
* If a visitor changes the content of a shopping cart (cart_changed=true, subtotal=<bedrag>, orderrows=[{product_id:<id>,quantity:<aantal>,price:<bedrag>}, ...])
* If a visitor does a checkout of the order (checkout=true)

* If a visitor visits the homepage (page_type=home)
* If a visitor visits a CMS page (page_type=info)
* If a visitor visits a category page (page_type=overview, category_id=<id>)
* If a visitor visits a product detail page (page_type=detail, product_id=<id>, category_id=<id>, <dimension>=<value>, ...)
* If a visitor visits the shopping cart (page_type=shoppingcart)
* If a visitor visits the order page (page_type=checkout)
* If a visitor visits the search result page (page_type=search, search=<zoekterm>)
* If a visitor visits the wish list (page_type=wishlist, products=[{product_id:<id>,category_id:<id>,<dimension>:<value>,...}])
* If a visitor visits the product comparison (page_type=compare, products=[{product_id:<id>,category_id:<id>,<dimension>:<value>,...}])

* If a visitor on product detail page clicks the tab Product properties (details=attributes)
* If a visitor on product detail page clicks the tab Reviews (details=reviews)
* If the filters on a category page are used by a visitor (filter=true, <dimension>=<value>, …)
* If the sorting on the category page is used (order=<dimension>, direction=asc/desc)

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


################
Get profile data
################

There are three ways to get a profile out of IQNOMY:

#. :ref:`Liquid Internet <profile-in-lc>`
#. :ref:`REST api <apidoc>`
#. :ref:`Active profile hooks <hooks>`


The main way to get the profile information from IQNOMY is by letting IQNOMY send this information to you. This can be done as a response on an action of a visitor or at the end of a session. 

Containers can also be used to get the IQNOMY profile, but this method is less used. Companies use this method if they want this information realtime available in the CMS for personalisation.


The extraction of the IQNOMY profile can be done through containers:

* The container will show liquid content
  * HTML
  * Javacript
  * JSON
  * XML

You can use liquid content that you define in the IQNOMY platform. Based on the visitors profile IQNOMY will show you the right content. You can also use build in liquid content that will show the profile of the visitor. This way you can request the container through REST or javascript with your own profile ID to get the profile information for your CRM.

.. todo::   * `Ook alle IQNOMY information in jou systemen (Dutch pdf) <http://www.iqnomy.com/downloads/handleidingen/ook_alle_IQNOMY_informatie_in_jouw_systemen.pdf>`_
.. todo::   * `IQNOMY liquid e-mail marketing cases (Dutch pdf) <http://www.iqnomy.com/downloads/cases/IQNOMY_liquid_e-mail_marketing_cases.pdf>`_

