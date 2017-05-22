.. include:: ../links.rst
   
#####
API's
#####

.. contents::

.. _apidoc:

We have :ref:`public <publicapi>` and behind :ref:`OAUTH2 <oauth2>` api's.

.. _oauth2:

#############################
Overview OAUTH2 REST services
#############################

The REST webservices start with the link: https://api.iqnomy.com or login in https://management.humanswitch.io and go to 'support' in the menu.

Authentication of webservices
=============================

We are using OAUTH2 for the authentication of our webservices.

You can test the REST service at https://api.iqnomy.com with your IQNOMY user account.

To request a token you can use the url:

* https://keycloak.iqnomy.com/auth/realms/IQNOMY/protocol/openid-connect/token
* client_id=iqnomy-paas

Step 1: request offline access
------------------------------
Stap 1: offline access aanvragen

The IQNOMY platform has a tenant structure. One user has access to 1 or more tenants.

POST https://keycloak.iqnomy.com/auth/realms/IQNOMY/protocol/openid-connect/token

You have to send once your username and password to request a token.

grant_type=password&client_id=iqnomy-paas&username={{username}}&password={{password}}&scope=offline_access

Example request
---------------

.. code-block:: HTML

  POST /auth/realms/IQNOMY/protocol/openid-connect/token HTTP/1.1
  Host: keycloak.iqnomy.com
  Content-Type: application/x-www-form-urlencoded
  Cache-Control: no-cache
  Postman-Token: bc1ba92f-da4c-a4c2-4a19-2551fbc02ec7

  grant_type=password&client_id=iqnomy-paas&username=c.vriens%40asknow.nl&password=!A1234567&scope=offline_access

Step 2. Grant refresh
---------------------
A refresh token has a 30 days expire date if it is not used. Then you will have to request a new grant.

With grant refresh you will get a new access token.

POST: https://keycloak.iqnomy.com/auth/realms/IQNOMY/protocol/openid-connect/token

Example
-------

.. code-block::

  POST /auth/realms/IQNOMY/protocol/openid-connect/token HTTP/1.1
  Host: keycloak.iqnomy.com
  Content-Type: application/x-www-form-urlencoded
  Cache-Control: no-cache
  Postman-Token: ac6ce6be-40a9-fe57-925b-d378954d9898

  grant_type=refresh_token&refresh_token={{refreshtoken}}&client_id=iqnomy-paas

Step 3. use the api
-------------------

The authentication of a service request is done with the use of the accesstoken as a bearer.

.. _eventapi:

##########
Public api
##########

Impressor api
=============

Request
-------

The impressor api is also used by the :ref:`websitescript` to register the profile events and request for liquid content.

.. code-block:: html

  https://liquifier.iqnomy.com/myliquidsuite-ws/async/impr/572b006153f4ee96fa8ab37bbca679ac?tenant=157078931&iqversion=4&fid=8&prid=AXxANA!!-GRHLWFS~LZ!LHFyk7SV7QArFyBWdXr439j2zlB9f&iqurl=https%3A%2F%2Fwww.humanswitch.io%2F&canonical=https%3A%2F%2Fwww.humanswitch.io%2F&iqeventdata=page%3Dfrontpage&jsonpTransport=flyjsonp_FCBDBADA2E48409F8097C3E899017B20

You can test this url by using it in you browser.

Example url
~~~~~~~~~~~

The example url from above in pieces:

* https://liquifier.iqnomy.com/myliquidsuite-ws/async/impr/572b006153f4ee96fa8ab37bbca679ac?
* tenant=157078931&
* iqversion=4&
* fid=8&
* prid=AXxANA!!-GRHLWFS~LZ!LHFyk7SV7QArFyBWdXr439j2zlB9f&
* iqurl=https%3A%2F%2Fwww.humanswitch.io%2F&
* canonical=https%3A%2F%2Fwww.humanswitch.io%2F&
* iqeventdata=page%3Dfrontpage&
* jsonpTransport=flyjsonp_FCBDBADA2E48409F8097C3E899017B20

URL explained
~~~~~~~~~~~~~

https://liquifier.iqnomy.com/myliquidsuite-ws/async/impr/**572b006153f4ee96fa8ab37bbca679ac**

The number in the url is a random hash. Validation at the server site is: {uuid:[0-9a-f]{32}}. So a string of 32 characters with 0-9 and a-f. Because of the scalability and stateless architecture this uuid is used to keep the request and response handling together. So it must be different for every request.

As an example in javascript the following function is used:

.. code-block:: javascript

  function() {
          var S4 = function() {
              return (((1 + Math.random()) * 0x10000) | 0).toString(16)
                      .substring(1);
          };
          return (S4() + S4() + S4() + S4() + S4() + S4() + S4() + S4());
	};

The parameters used in the url are.

  tenant
    The id of the account where you are sending the the request.

  iqversion
    4 is the version of the impressor request you implemented.

  fid
    A random number between 0 and 100 used for loadbalancing.

  iqurl
    Url is used to check where the reponse is coming from and if the request is from a valid domain. The domain in this url must be validated in management of the platform.

  prid
    The profile id. If no profile id is in the request then the reponse will give you a new profile id.

  canonical
    Can be used as a normalized url.

  referrer
    The referrer url is can be set here.

  iqeventdata
    You can send custom key values as an event property.

  jsonpTransport
    This is a callback function name for jsonp. The is only used in clientside jsonp script and can be removed if you don't use it.

  sync
    Without this the request is always async. This variable can be set as sync=true. This means you get only 1 reponse. If you have multiple impressions implemented on this url you will get all the impressions in this reponse.

Response
--------

The response example below has containers as a response with both one liquid content.

.. code-block:: javascript

    callback ({
     "containerImpressions":[
        {
           "imprElements":[
              {
                 "htmlTemplate":"<a href=\"https://management.test.iqnomy.com/management?lqcid=004a47fc-7890-4354-ad70-2c8a60974bd1-1-0\" title=\"logoooo\"><img src=\"\" border=\"0\">\n  \ttest\n    <div class=\"testStyle2\">\n        <table>\n            <tr>\n                <th>Beschrijving</th>\n                <th>Content E</th>\n            </tr>\n            <tr>\n                <th>Container</th>\n                <th>2364</th>\n            </tr>\n            <tr>\n                <td>Liquidcontent</td>\n                <td>26347</td>\n            </tr>\n            <tr>\n                <td>SelectionMethod</td>\n                <td>Personalisatie: Geen!</td>\n            </tr>\n            <tr>\n                <td>Fallback</td>\n                <td>Yes</td>\n            </tr>\n        </table>\n    </div>\n</a>\n",
                 "description":"",
                 "id":"26350",
                 "name":"logoooo",
                 "url":"nvt?lqcid=004a47fc-7890-4354-ad70-2c8a60974bd1-1-0",
                 "lqcid":"004a47fc-7890-4354-ad70-2c8a60974bd1-1-0",
                 "order":0,
                 "score":1,
                 "uuid":"a0d75cea-b845-45d8-a2c2-063ba693f3e3"
              }
           ],
           "container":{
              "dateCreated":"2015-05-13T15:56:23+02:00",
              "description":"Test container for MLS-2274 to test a container based on a feed and a resource",
              "id":2366,
              "name":"Test Container (2366) - Banner Feed - MLS-2274"
           },
           "postInjectionScript":"",
           "preInjectionScript":"var _iqContentBox2 = document.createElement('div');\r\n_iqContentBox2.id = '_iqContentBox310';\r\n_iqContentBox2.style.display = 'block';\r\n_iqContentBox2.style.position = 'fixed';\r\n_iqContentBox2.style.bottom = '15px';\r\n_iqContentBox2.style.left = '15px';\r\n_iqContentBox2.style.padding = '10px';\r\n_iqContentBox2.style.border = '1px solid black';\r\n\r\ndocument.getElementsByTagName('body')[0].appendChild(_iqContentBox2);\r\n",
           "xpath":"//div[@id=\"_iqContentBox310\"]"
        },
        {
           "imprElements":[
              {
                 "htmlTemplate":"<a href=\"javascript:window.location.href=window.location.href + '?lqcid=004a47fc-7890-4354-ad70-2c8a60974bd1-0-0'\" title=\"Content A\"> <img src=\"https://www.test.iqnomy.com/iq-demo/management.test/demo/container_2364/liquidcontent_responsive_img2.jpg\" border=\"0\">\r\n    <div class=\"testStyle2\">\r\n        <table>\r\n            <tr>\r\n                <th>Beschrijving</th>\r\n                <th>Content A</th>\r\n            </tr>\r\n            <tr>\r\n                <th>Container</th>\r\n                <th>2364</th>\r\n            </tr>\r\n            <tr>\r\n                <td>Liquidcontent</td>\r\n                <td>26344</td>\r\n            </tr>\r\n            <tr>\r\n                <td>SelectionMethod</td>\r\n                <td>A/B</td>\r\n            </tr>\r\n            <tr>\r\n                <td>Fallback</td>\r\n                <td>No</td>\r\n            </tr>\r\n        </table>\r\n\r\n    </div>\r\n</a>\r\n<style>\r\n    #_iqContentBox2 {\r\n        position: fixed;\r\n        left: 0;\r\n        top: 0;\r\n        max-width: 200px;\r\n    }\r\n    \r\n    .testStyle2 {\r\n\t\ttext-align: left;\r\n\t\tposition: absolute;\r\n\t\ttop: 0;\r\n\t\tleft: 0;\r\n\t\twidth: 100%;\r\n\t\tbackground: rgba(0,0,0,0.5);\r\n\t\theight: 100%;\r\n\t\tcolor: #FFFFFF;\r\n\t\tfont-weight: bold;\r\n\t}\r\n\t\r\n\t#_iqContentBox2 .testStyle2 table{\r\n\t\tmargin: 20px 5px;\r\n\t}\r\n</style>",
                 "description":"TestContainer1-ContentA-AB-No-Fallback",
                 "id":"26344",
                 "name":"TestContainer1-ContentA-AB-No-Fallback",
                 "url":"?lqcid=004a47fc-7890-4354-ad70-2c8a60974bd1-0-0",
                 "lqcid":"004a47fc-7890-4354-ad70-2c8a60974bd1-0-0",
                 "order":0,
                 "score":1,
                 "uuid":"a3134bbe-4050-4ff8-90b3-e9f3bef583da"
              }
           ],
           "container":{
              "dateCreated":"2015-05-12T13:51:57+02:00",
              "description":"",
              "id":2364,
              "name":"Test Container (2364) - Info logo - Links Boven - Fixed 100%"
           },
           "postInjectionScript":"var containerInfo = JSON.stringify(containerImpression.container,null,2);\r\nvar divContainerInfo = jQuery(\"<div><div class='testStyle2'></div></div>\");\r\ndivContainerInfo.css(\"position\",\"fixed\");\r\ndivContainerInfo.css(\"top\",\"200px\");\r\ndivContainerInfo.css(\"left\",\"0px\");\r\ndivContainerInfo.find(\".testStyle2\").text(containerInfo);\r\ndivContainerInfo.find(\".testStyle2\").css(\"position\",\"relative\");\r\ndivContainerInfo.find(\".testStyle2\").css(\"width\",\"200px\");\r\njQuery(\"body\").append(divContainerInfo);\r\n",
           "preInjectionScript":"jQuery('body').append('<div id=\"_iqContentBox2\"></div>');",
           "xpath":"//*[@id=\"_iqContentBox2\"]"
        }
     ],
     "eoi":true,
     "followId":36,
     "profileId":"AXxQLA!!-cYFeiA9ZPreMJmEUdn1o!h!WUXnokRRUdd2wlLT7"
  })

Explain response
~~~~~~~~~~~~~~~~

The response exists of a function callback({json response}). Within the function the json is set.

.. code-block:: javascript

  {
     "containerImpressions":[
        {
           "imprElements":"Array of liquid contents in this impression element. The result can be configured in management"[
              {
                 "htmlTemplate":"The HTML of the liquid content",
                 "description":"Description of the liquid content",
                 "id":"ID of liquid content",
                 "name":"Name of liquid content",
                 "url":"URL of liquid content or nvt+lqcid",
                 "lqcid":"Unique id to register the use (click) on this liquid content.",
                 "order":"Integer to give the order of the liquid content against other liquid contents in this impression element",
                 "score":"Integer with te score of this content.",
                 "uuid":"Unique id of the impression."
              }
           ],
           "container":{
              "dateCreated":"Container creation date",
              "description":"Container description",
              "id":"Integer with unique container id",
              "name":"Name of the container"
           },
           "postInjectionScript":"If configured extra code for post injection",
           "preInjectionScript":"If configured extra code for pre injection",
           "xpath":"Used to define where to use this impression in the DOM"
        },
        {
           "imprElements":"second impression in this response"[
              {
                 "htmlTemplate":"",
                 "description":"",
                 "id":"",
                 "name":"",
                 "url":"",
                 "lqcid":"",
                 "order":,
                 "score":,
                 "uuid":""
              }
           ],
           "container":{
              "dateCreated":"",
              "description":"",
              "id":,
              "name":""
           },
           "postInjectionScript":"",
           "preInjectionScript":"",
           "xpath":""
        }
     ],
     "eoi":"Boolean set to true if this is the end of the reponse",
     "followId":"Integer can be used as fid random generated by server. This is a number between 0-100 for loadbalancing",
     "profileId":"The unique profile id with this profile. If no profile id was set with the request a new profile id will be generated"
  })


register the click a liquid content
-----------------------------------

A click on a liquid content can be registered by adding lqcid=004a47fc-7890-4354-ad70-2c8a60974bd1-1-0 as a parameter to the url.

Example click in iqurl
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: html

  https://liquifier.iqnomy.com/myliquidsuite-ws/async/impr/c54f5f443502d52cfe7dfd49a65f8574?tenant=157078931&iqversion=4&fid=8&prid=AXxANA!!-GRHLWFS~LZ!LHFyk7SV7QArFyBWdXr439j2zlB9f&iqurl=https%3A%2F%2Fwww.humanswitch.io%2F%3Flqcid%3D004a47fc-7890-4354-ad70-2c8a60974bd1-1-0&canonical=https%3A%2F%2Fwww.humanswitch.io%2F&iqeventdata=page%3Dfrontpage&jsonpTransport=flyjsonp_345C2CD754064B9B801322EABB2F34B1

iqurl=https%3A%2F%2Fwww.humanswitch.io%2F%3Flqcid%3D004a47fc-7890-4354-ad70-2c8a60974bd1-1-0

Trackevent api
==============

The trackevent api is similar to the impressor api, but will not calculate an impression (So no container result). The standard response of a browser is at the moment in XML. If you send in the header request 'accept':'application/json' the response will be in json.

The impression api will automaticly generate a pagevisit. The trackevent api has two types of events you can use: FORM or WEBSHOP.

example url
~~~~~~~~~~~

.. code-block:: html

  https://liquifier.iqnomy.com/myliquidsuite-ws/async/trackevent/896de3356e30e1b18ec2ac8ba32c4090?tenant=157078931&iqversion=4&fid=8&prid=AXxANA!!-GRHLWFS~LZ!LHFyk7SV7QArFyBWdXr439j2zlB9f&iqurl=https%3A%2F%2Fwww.humanswitch.io%2F&canonical=https%3A%2F%2Fwww.humanswitch.io%2F&iqeventname=FORM&iqeventdata=firstname%3Dchristian&jsonpTransport=flyjsonp_9504F46F925345F1BB544E26FFEA5780

URL explained
~~~~~~~~~~~~~

Difference with impressor api is in the start of the url: https://liquifier.iqnomy.com/myliquidsuite-ws/async/trackevent

And the additional parameter: iqeventname=FORM

The iqeventname can be FORM or WEBSHOP. The name of the event in the livestream is depending on this. But technically there is no difference.

Profile api
===========

The path of the Profile public REST API call is: https://myliquidsuite-api.iqnomy.com/api/liquidaccount/
{liquidaccountId}/profile/cookie/{profileId}?includeSessions={sessionCount}&includeEvents={eventCount}.

This call returns the requested profile by its liquidaccountid and profileid.
Where the following parameters has to be given:

  {liquidaccountId}
    the id of the liquidaccount.
  {profileId}
    the id of the requested profile. The value of the cookie named _iqprid
  {sessionCount}
    The number of sessions included in the profile. For performance set it -1 (no sessions beeing returned because they are not needed)
  {eventCount}
    The number of sessions included in the profile. For performance set it -1 (no events beeing returned because they are not needed)

The profile that is returned will have the following structure (the non relevant data is omitted) :

.. code-block:: json

  {
     "id":"AXqObQ!!-O8OgevKhqjfiiidWRSLevIzyo02ki2iCH31aU2yP",
     "dateCreated":"2017-03-03T12:29:37.000+0000",
     "dateLastSeen":"2017-04-06T12:13:30.000+0000",
     "lastSession":{
     },
     "lastResource":{
     },
     "sessionCount":34,
     "clickCount":0,
     "pagevisitCount":92,
     "online":true,
     "value":5,
     "dimensionProperties":[
     ],
     "properties":[
        {
           "name":"last_watched_objects",
           "value":"26123,399177,26123,36457"
        },
        {
           "name":"visitorHasExternalId",
           "value":"true"
        },
        {
           "name":"profile.ids.mc_eid",
           "value":"eb4f8ef7bf"
        }
     ],
     "sessions":null
  }


Magento api
===========

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



