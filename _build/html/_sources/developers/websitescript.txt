.. _websitescript:

##############
Websitescript
##############

.. contents::

**************************
Basic script functionality
**************************

Standard tracking script implementation
=======================================

Standard implementation of the script can be done by a webmaster. He will implement the script in the source code of your website. Normally this is done in a website template.

* Asynchronious to prevent page loading problems
* Can be placed with the Google tagmanager
* Should be on every page where you want to follow your customers


BODY script
===========

Make sure the BODY script is placed in between the body tags. Normally a tracking script is being implemented just before the </body>.

.. image:: _static/images/BODYScript.png

Every BODY script has a customer specific number! Yours is in the email you receive after registering a MyLiquidSuite.

Check if the script is implemented
==================================

If the standard script is implemented you can check this yourself by opening your website in you browser. Right-click your mouse and open 'source website'.

When you see the source of your website you can check by search in this txt for 'iqnomy'. If you search in the txt for 'iqnomy' this will show you the BODY-script.

If IQNOMY tells you that you are still not connected check if the number in the BODY-script is the same as the number in your Liquid Account. Still problems then email us at support@iqnomy.com

**********************
Visitor identification
**********************

For each visitor, IQNOMY uses a unique visitor id to track the pagevisits of a visitor on a tenants website.
To have more insight into who is visiting your website you can link an custom external id to the visitor.
There are 3 options available to do this.

Basic visitor identification
============================
The id of the visitor will be set in a cookie

Custom id's
===========

Option 1: a global Javascript variable
--------------------------------------

To add an custom id to an IQNOMY visitor you can add a global Javascript variable _iqExternalVisitorId to your webpage. The Javascript variable will be processed by the IQNOMY script and the value will be linked to the visitor.
Make sure that the variable is initiated on the webpage before the IQNOMY is processed, otherwise the _iqExternalVisitorId will not be processed automatically.

.. code-block:: javascript

 <script type="text/javascript">
      var _iqExternalVisitorId = "company_user_id_1"; </script>

Option 2 HTML query string paramameter
--------------------------------------

Alternatively you can add a HTML query string paramameter, _iqExternalVisitorId,to your webpage url. The value of the parameter will be linked to the visitor and can be used as the external visitor id.
Contact us if you want to use this method, so that we can enable this feature.

.. code-block:: javascript

   www.mywebsite.com/home?_iqExternalVisitorId=company_user_id_1

Option 3: using the IQImpressor Javascript object
-------------------------------------------------
You can also assign the external id manually. By using the IQImpressor Javascript object, available after the IQNOMY script is initiated, you can manually track an event. By calling
IQImpressor.trackEvent(tenantId,eventName,eventdata) you can trigger an event that will link a custom external id, to the visitor visiting your website.

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

We advice not to use any privacy-sensitive custom id as an external id, like emailadresses.

*******************
Extra functionality
*******************

Xpath finder
============

Solution
An URL extended with a link where the user can open the webpage to select the location of the page.

An url-argument is automatically added to the url **iqxpselect=true**, this will trigger the xpath-selection javascript included in the impression-script.

Preview with underline
======================
Add the parameters:
iqprvw and iqprvwborder to your url.

.. note::
   iqprvw=(containerid):(liquidcontentid):(xpath)

Example:

.. code-block:: javascript

   URL?iqprvw=1791:16608://div[@id="liquid"]&iqprvwborder=1


You can also make use of the IQNOMY api and create your own javascript plugin. For more information contact support@iqnomy.com

Cross domain tracking
=====================

Companies can use there own identification accross domains. Also the IQNOMY id can be used accross domains.

Usage
-----

When you are on the www.vangilscomputer.nl and click a link that goes to the domain www.vangilscomputers.com. This is a different domain.

Add the new function IQImpressor.linkVisitor(this); to a onclick event of a link:

.. code-block:: javascript

   <a href="http://www.vangilscomputers.com/" onclick="IQImpressor.linkVisitor(this);">www.vangilscomputers.com</a>

When the user clicks on the link, this function will add two query-parameters to the url of the link, example: http://www.vangilscomputers.com/?&_iqnomyvids=1234&_iqnomyfids=4.

On the target page, these parameters will be read by our script and will create two session cookies with these values.
Our impression-script will prefer to use the visitor-id/follow-nr from the session cookies.

The function linkVisitor(obj) accepts different types of the obj param.

* For an a href-object, it will use the a.href field to manipulate the url.
* For a form-object, it will use the form.action field to manipulate the url.
* For a string-object, it will append the parameters to the string.
* In all cases, it will return the manipulated url when succeeded.

Considerations
--------------

* both domains should be approved in the website-list (like always)
* both domains should contain the same integration script with the same tenant-id
* the visitor will be followed across the other domain for this session only.
* link with a hash-character might not work correctly
* might conflict with other scripts on the website

.. note::
   It can conflict with _gaq.push() when setAllowLinker=true is used in the Google script.

**********************
Customizing the script
**********************

Client side liquid internet
===========================

Client site the liquid container. You need to put the container id and the xpath id in the script. 

.. code-block:: javascript
   :linenos:

   <script>                               
   var _iqnomytenant = XXXXXXXXX;
   var _iqnomyImpress = { hostAndPort: "tracker.iqnomy.com", timeout: 5000, debug : true, containers : [
              { id : 913 ,xpath : '//*[@id="liquidontainer913"]'}
              ]};
   (function() {
   var _iqs = document.createElement('script'); _iqs.type = 'text/javascript'; _iqs.async = true;
   _iqs.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'static.iqnomy.com/myliquidsuite/js/IQImpressor.js';
      var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(_iqs, s);
    })();
   </script>

Tracking mailto
===============

* JQuery in the page header, example use the next rule in the <head> of the page:

.. code-block:: javascript

   <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>

* Put in the iqnomy script the next variable:

.. code-block:: javascript

   var iqTrackMailto = true; 

Synchronous script
==================

The standard script is asynchronous. But you can make it synchronous.

Change in the basic script _iqs.async = true to _iqs.async = false
	
Website listener
================

Data in the webform is send when the form is submitted. 

JQuery should be loaded, so put it in the page header:

.. code-block:: javascript

   <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>

Set script variable '_iqTrackForm' as 'true'

.. code-block:: javascript

   <script>
   var _iqTrackForm = true;
   </script>

External visitor id
===================

Read more: Identifying iqnomy visitors using custom id

Extra custom javascript script
==============================

We can add extra custom javascript with the existing script. To get this extra javascrip you need to add an extra rule with the existing script. 

.. code-block:: javascript

   var _iqsExtra = true;
 
.. warning::

   Pay attention: before adding this rule the script needs to be available on the IQNOMY servers. You can check this with the URL:
 
.. code-block:: javascript

   http://static.iqnomy.com/myliquidsuite/js/tnt/pre_<tenantId>.js

*Complete example*

.. code-block:: javascript

   <script>
     var _iqsTenant = <tenantId>;
     var _iqsImpress = { hostAndPort: "liquifier.iqnomy.com", timeout: 5000 };
     var _iqsExtra = true;
     
     (function() {
       var _iqs = document.createElement('script'); _iqs.type = 'text/javascript'; _iqs.async = true;
       _iqs.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'static.iqnomy.com/myliquidsuite  /js/IQImpressor.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(_iqs, s);
     })();
   </script>

.. _scripteventdata:

**********
Event data
**********

Different methods
=================

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

Testing with event data
=======================
You can test this functionality in the console of your webbrowser. The results can be checked in the livestream.

.. figure:: _static/images/EventData.png

################
Filter IP adress
################

In *Discovery* you can got to *IP-addresses*

With this functionality you can filter based on ip-adress. After setting the filter the caching should be up to date after 10 minutes.

You can use the settings:
* Don't filter (standard)
* Exclude all but this ip
* Accept all but this ip

You can use ranges


* Example 1: IQNOMY office extern (clients 193.172.34.65 t/m 193.172.34.78)

IP-adress: 193.172.34.64
subnetmasker: 255.255.255.240

* Example 2: One specific IP-adress

IP-adress: 193.172.34.66
subnetmasker: 255.255.255.255

Also IPv6 addresses can be used

* Example 3: One specific IPv6-adress

IP-adress: fe80::c0f3:5b08:37d9:6e90
subnetmasker: fe80::c0f3:5b08:37d9:6e90

* Example 4: range IPv6

IP-adress: fe80::
subnetmasker: fe80::

For ranges you can use: http://www.subnet-calculator.com/

