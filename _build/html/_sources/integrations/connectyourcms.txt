To connect your CMS content with IQNOMY you can use our webservices. See [[webservices]] for the authentication.

http://liquifier.iqnomy.com/myliquidsuite-ws/LiquidContainerService?WSDL

=createResourceCollection=
==Request==
 <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ser="http://com.iqnomy.liquidplatform/liquidcontainer/service">
   <soapenv:Header/>
   <soapenv:Body>
      <ser:createResourceCollection>
         <resourceCollection name="Company Banner wst1">
            <!--Zero or more repetitions:-->
            <attributeDefinition name="naam" type="STRING" identifier="true" language="false" content="false" expression="" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="doellink" type="STRING" identifier="false" language="false" content="false" expression="" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="pageplacement" type="STRING" identifier="false" language="false" content="false" expression="" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="title" type="STRING" identifier="false" language="false" content="false" expression="" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="mainImage" type="STRING" identifier="false" language="false" content="false" expression="" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="language" type="EXPRESSION" identifier="false" language="true" content="false" expression="'DUTCH'" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="content" type="STRING" identifier="false" language="true" content="true" expression="" dateformat="" expiredate="false" activatedate="false"/>
            <attributeDefinition name="einddatum" type="DATE" identifier="false" language="false" content="false" expression="" dateformat="dd/MM/yyyy" expiredate="true" activatedate="false"/>
            <attributeDefinition name="startdatum" type="DATE" identifier="false" language="false" content="false" expression="" dateformat="dd/MM/yyyy" expiredate="false" activatedate="true"/>
         </resourceCollection>
      </ser:createResourceCollection>
   </soapenv:Body>
 </soapenv:Envelope>

==Response==

=addKeyValueResource=
==Request==
 <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ser="http://com.iqnomy.liquidplatform/liquidcontainer/service">
   <soapenv:Header/>
   <soapenv:Body>
      <ser:addKeyValueResource>
         <resourceCollectionId>63</resourceCollectionId>
         <keyValue>
            <name>naam</name>
            <value>Z10</value>
         </keyValue>
         <keyValue>
            <name>doellink</name>
            <value>http://www.company.com/shop</value>
         </keyValue>
         <keyValue>
            <name>pageplacement</name>
            <value>pageplacement=IQ_MV_CNP2</value>
         </keyValue>
         <keyValue>
            <name>title</name>
            <value>Shop at this company</value>
         </keyValue>
         <keyValue>
            <name>mainImage</name>
            <value>http://pages.company.com/aanbieding/image/iq/MV_CN3.jpg</value>
         </keyValue>
         <keyValue>
            <name>content</name>
 <value>

 Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in  reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in  culpa qui officia deserunt mollit anim id est laborum.
 </value>
         </keyValue>
         <keyValue>
            <name>einddatum</name>
            <value>5/5/2013</value>
         </keyValue>
         <keyValue>
            <name>startdatum</name>
            <value>1/4/2013</value>
         </keyValue>
      </ser:addKeyValueResource>
   </soapenv:Body>
 </soapenv:Envelope>

==Response==

=createLiquidContainerFeed=
==Request==
 <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ser="http://com.iqnomy.liquidplatform/liquidcontainer/service">
   <soapenv:Header/>
   <soapenv:Body>
      <ser:createLiquidContainerFeed>
         <liquidContainerFeed>
            <condition>true</condition>
            <htmlTemplate><![CDATA[

<div class="cp_content_top">
<p>
<a href="$doellink?$impressionUrlParam&$pageplacement"
title="$title">
<img src="$mainImage" border="0">
</a>
</p>
</div>
            ]]></htmlTemplate>
            <liquidContainerId>1814</liquidContainerId>
            <name>x7 feed</name>
            <!--Optional:-->
            <resourceCollectionId>63</resourceCollectionId>
         </liquidContainerFeed>
      </ser:createLiquidContainerFeed>
   </soapenv:Body>
 </soapenv:Envelope>

==Response==

=touchResourceCollection=
==Request==
 <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ser="http://com.iqnomy.liquidplatform/liquidcontainer/service">
   <soapenv:Header/>
   <soapenv:Body>
      <ser:touchResourceCollection>
         <resourceCollectionId>63</resourceCollectionId>
      </ser:touchResourceCollection>
   </soapenv:Body>
 </soapenv:Envelope>



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

=Standard leisure layout=

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

=Custom layout=
If you want a custom layout you can contact us at support@iqnomy.com

