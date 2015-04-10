##############
Software hooks
##############

The IQNOMY platform can provide two hooks.

#. Based on a profile event
#. End of session

Profile event hook
==================

End of session hook
===================


************
JSON profile
************

DOM-model Visitor (raw)
=======================

.. code-block:: json

   {
   	"id": 0,
   	"tenant": 0,
   	"externalid":"",
   	"sessioncount":0,
   	"pagevisitcount":0,
   	"datelastvisited":"",
   	"properties": [
   	  {
   	    "name":"",
   	    "value":""
   	  }
     ],
     "dimensions":[
       {
         "name":"",
         "value":"",
         "weight":0.0
       }
     ],
     "session":{
       "datecreated":"",
       "dateexpired":"",
       "referrerLocation":"",
       "event":{
         "type":"",
         "properties":[
       	  {
       	    "name":"",
       	    "value":""
       	  }
         ]
       }
     }
   }

DOM-model Visitor (description)
===============================

() is used to describe the JSON property and is not part of the value of the property.

.. code-block:: json

   {	(object,required, The visitorobject)
   	"id": (long,required, The id of the visitor),
   	"tenant": (integer,required, The id of the tenant),
   	"externalid": (string,optional, An external id that can be used to identify with a external reference,e.g. email),
   	"sessioncount": (integer,required, The number of sessions the visitor has),
   	"pagevisitcount": (integer,required, The number of pagevisits the visitor has),
   	"datelastvisited": (string,required, The number of pagevisits the visitor has, with format "dow mon dd hh:mm:ss zzz yyyy"),
   	"properties": (array,required, An array of visitorproperty objects, with a size min of 0 and max of 2,147,483,647)
   	[
   		{	(object,optional, A visitorproperty set in a rule with the visitor as context)
   			"name": (string,required, The name of the visitor property),
   			"value": (string,required, The value of the visitor property)
   		}
   	],
   	"dimensions": (array,required, An array of dimensions, with a size min of 0 and max of 2,147,483,647)
   	[
   		{	(object,optional, A dimension that represents a state the visitor has while retrieving this visitor object)
   			"name": (string,required, The name of the dimension),
   			"value": (string,required, The value of the dimension)
   			"weight": (double,required, The weight of the dimension)
   		}
   	],
   	"session": (object,required, The current session of the visitor)
   	{
   		"datecreated":(string,required, The creation date of the session as a String using the dateformat, "dow mon dd hh:mm:ss zzz yyyy"),
   		"dateexpired":(string,optional, The expire date of the session as a String using the dateformat, "dow mon dd hh:mm:ss zzz yyyy" . Will be null when the session is not expired),
   		"referrerLocation":(string,optional, The creation date of the session as a String using the dateformat,"dow mon dd hh:mm:ss zzz yyyy"),
   		"event": (object,optional, The event that occured during the session and is the trigger for creating/sending this visitorobject)
   		{
   			"type":(string,required, An enum value of the type of the event represented as a String. possible values: pagevisit,formsubmit,webshop,iquery,impressionclick),
   			"properties": (array,required, An array of properties set in a rule with the rule as context, with a min of 0 and max of 2,147,483,647),
   			[
   				{	(object,optional, An eventproperty that represents a state of the event has when it occured)
   					"name": (string,required, The name of the session property),
   					"value": (string,required, The value of the session property)
   				}
   			]
   		}
   	}
   }

REST requirements
=================

REST service requirement for pushing visitor data
- POST method that is HTTP 1.1 compliant
- POST method has no url argument
- Optional POST method uses basic authentication
- JSON will be posted as body
- proper return codes,e.g 200 ok, 401 not authorized

Examples
========

fully populated
---------------

Fully populated json profile

.. code-block:: json

   {
      "id": 2184230412,
      "tenant": 2456524,
      "externalid": "steven@iqnomy.com",
      "sessioncount": 1,
      "pagevisitcount": 10,
      "datelastvisited": "Fri Aug 29 11:15:47 CEST 2014",
      "properties": [
         {
            "name": "page_type",
            "value": "overview"
         },
         {
            "name": "product_id",
            "value": "3527"
         }
      ],
      "dimensions": [
         {
            "name": "Count of visits:",
            "value": "10",
            "weight": 1
         },
         {
            "name": "Coupon code use (by visitor):",
            "value": "No coupon",
            "weight": 2
         }
      ],
      "session": {
         "datecreated": "Thu Aug 28 11:15:47 CEST 2014",
         "dateexpired": "Fri Aug 29 11:18:47 CEST 2014",
         "referrerLocation": "http:\/\/www.google.nl",
         "event": {
            "type": "pagevisit",
            "properties": [
               {
                  "name": "page_type",
                  "value": "overview"
               },
               {
                  "name": "product_id",
                  "value": "3527"
               }
            ]
         }
      }
   }

Empty arrays
------------
If no values are available arrays can be empty.

.. code-block:: json

   {
      "id": 2184230412,
      "tenant": 2456524,
      "externalid": "steven@iqnomy.com",
      "sessioncount": 1,
      "pagevisitcount": 10,
      "datelastvisited": "Fri Aug 29 11:15:47 CEST 2014",
      "properties": [],
      "dimensions": [],
      "session": {
         "datecreated": "Thu Aug 28 11:15:47 CEST 2014",
         "dateexpired": "Fri Aug 29 11:18:47 CEST 2014",
         "referrerLocation": "http:\/\/www.google.nl",
         "event": {
            "type": "pagevisit",
            "properties": []
         }
      }
   }

Null value (dateexpired)
------------------------
If a eventhook is used, it can happen that the session date expired is still null.

.. code-block:: json

   {
      "id": 2184230412,
      "tenant": 2456524,
      "externalid": "steven@iqnomy.com",
      "sessioncount": 1,
      "pagevisitcount": 10,
      "datelastvisited": "Fri Aug 29 11:15:47 CEST 2014",
      "properties": [],
      "dimensions": [],
      "session": {
         "datecreated": "Thu Aug 28 11:15:47 CEST 2014",
         "dateexpired": null,
         "referrerLocation": "http:\/\/www.google.nl",
         "event": {
            "type": "pagevisit",
            "properties": []
         }
      }
   }


