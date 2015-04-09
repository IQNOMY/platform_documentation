##########
Event data
##########

****************************************
Connect information with visitor profile
****************************************

Input of information into the visitor profile can be used if other information is being gathered about this user. 

Example
=======
* CRM information
* Information about from campaigns 
* Other identifiers
* Form input
* Profiles from other applications
* etc.

Make sure that the things you do are legal looking at privacy of your anonymous visitor. It's your responsibility that the visitors privacy is being respected. We can disconnect IQNOMY if we suspect any legal rights are being violated. 

Gathering data:
* Using a javascript as trackingpixel the data can be put into the URL. We will receive this URL visited and extract this data. e.g. http://www.iqnomy.com/index.html?Campaign_data=name_of_campaign
* If you don't want the visitor to see this information you can put the data into the URL that is being used in the javascript. It can be different from the URL the visitors see in their browsers. The visitor can still see the information when he looks into the page source. 
* A third option is to use webservices

Methods to register data
========================

There are 3 ways to add data to the profile:
# [[Webservices#REST|REST api]]
# Page-load
# TrackEvent

Example 1 - Sending eventdata at pageload
-----------------------------------------

prerequisite: The eventdata needs to be set and available before the IQNOMY script is loaded

.. code-block:: javascript 

   <script>

   _iqsEventData = new Object();
   _iqsEventData["page_type"] = “home”

   </script>

Example 2 - Sending eventdata manually 
--------------------------------------

From the client using javascript

prerequisite:  The IQNOMY script needs to be loaded before able to call functions on the IQImpressor object.

.. code-block:: javascript 

   <script>
   
   var eventData = new Object();
   eventData["page_type"] = “home”
   IQImpressor.trackEvent(_iqsTenant, 'WEBSHOP', eventData); 
   
   <script>

Example 3 - Combine sending eventdata at pageload and sending it manually
-------------------------------------------------------------------------

If you are unsure when the eventdata is available during the pageload you can use this option to be sure eventdata will be send to IQNOMY

.. code-block:: javascript

   <script>
   
   var eventData = new Object();
   eventData["page_type"] = “home”;
   
   // If IQNOMY script is not loaded let the script pickup the data when the script loads
   if(typeof IQImpressor === "undefined") {
       _iqsEventData = eventData;
       console.log("Saving EventData to be picked up later.");
   // Else send it manually
   }else{
       IQImpressor.trackEvent(_iqsTenant, 'WEBSHOP', eventData);
       console.log("Sending EventData manually.");
   }
   
   <script>

Custom events
=============

This example is also used in [[Identifying_iqnomy_visitors_using_custom_id]]
You can also assign the external id manually. By using the IQImpressor Javascript object, available after the IQNOMY script is initiated, you can manually track an event. By calling
IQImpressor.trackEvent(tenantId,eventName,eventdata) you can trigger an event that will link a custom external id, to the visitor visiting your website.

example:
 
.. code-block:: javascript

   <script type="text/javascript">
 
       var tenantId = _iqsTenant
       var eventName = 'FORM'
       var eventdata = new Object();
           eventdata["_iqExternalVisitorId"] = "company_user_id_1";
 
       // You can only call this function after the IQNOMY has initialised.
       IQImpressor.trackEvent(tenantId,eventName,eventdata);
 
       var _iqExternalVisitorId = "company_user_id_1"; </script>


You can use both methods combined, but make sure that the given custom id is consistent, or external id of the visitor will change with the use of each method. Currently a IQNOMY user can only have one unique external id.

IQNOMY tracks visitors anonymously, so we advice not to use any privacy-sensitive custom id as an external id, like emailadresses.

Multiple events
---------------

.. code-block:: javascript

   var eventData = new Object();
   
   eventData["name"] = “christian”
   eventData["customer"] = “true”
   eventData["productid"] = “40”
   IQImpressor.trackEvent(_iqsTenant, 'WEBSHOP', eventData);

REST API
========

Standard key / values
---------------------

IQNOMY can use a standard set of key values. Based on those key/values standard rules are used. The key values will be connected in the IQNOMY platform in the right way to the user. The values are used also in the [[IQNOMY Magento extension]].

==========================
Ecommerce site integration
==========================

Our IQNOMY script can already track a lot on the website. But to make tracking even better and richer we provide the following layouts:
* [[#Standard webshop layout|Standard webshop layout]]
* [[#Standard leisure layout|Standard leisure layout]]
* [[#Custom layout|Custom layout]]

For [[IQNOMY_Magento_extension|Magento]] we already created our standard plugin that does this. 

If you want to know how you can register these standard layouts. Read more in [[Register_event_data]]

=Standard webshop layout=
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
