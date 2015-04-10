#######
Profile
#######

Profile id
==========

.. glossary::
   Profile
     The profile is based on a unique identification together with properties and connected eventproperties that can be grouped by an session

Connect your id with the IQNOMY profile
=======================================

If you want to recognize a visitors profile based on your id. You can connect your id with the iqnomy profile. This way you can use your id to identify the visitor.

It works two ways:

* IQNOMY can use the information you have with your id in the IQNOMY profile. 
* Based on your ID you can extract information from the IQNOMY platform.

.. seealso:: 
   
   `Add data to profile`
      Add extra data to the profile so you can use it later
    
   Identifying iqnomy visitors using custom id

Examples for your ID can be:

* emailid from the emailmarketing system
* your CRM id
* the login id from your website


Add information to the IQNOMY profile
=====================================

You can add information into the IQNOMY profile of your visitor.

Examples can be:

* Extra information from your CRM
* Emailmarketing information
* SEA information
* SEO information

If you send an emailmarketing newsletter, put extra information into the links of you newsletter. This can be an example of the productcategory, age of the receiver, name of the receiver, etc. Example: http://www.iqnomy.com/blog/?name=christian. In this example the IQNOMY profile now knows the name of the visitor.

:ref:`Register event data <events>`


Get profile information out of the IQNOMY platform
==================================================

The main way to get the profile information from IQNOMY is by letting IQNOMY send this information to you. This can be done as a response on an action of a visitor or at the end of a session. 

Containers can also be used to get the IQNOMY profile, but this method is less used. Companies use this method if they want this information realtime available in the CMS for personalisation.


The extraction of the IQNOMY profile can be done through containers:

* The container will show liquid content
  * HTML
  * Javacript
  * JSON
  * XML

You can use liquid content that you define in the IQNOMY platform. Based on the visitors profile IQNOMY will show you the right content. You can also use build in liquid content that will show the profile of the visitor. This way you can request the container through REST or javascript with your own profile ID to get the profile information for your CRM.

.. seealso::
   * `Ook alle IQNOMY information in jou systemen (Dutch pdf) <http://www.iqnomy.com/downloads/handleidingen/ook_alle_IQNOMY_informatie_in_jouw_systemen.pdf>`_
   * `IQNOMY liquid e-mail marketing cases (Dutch pdf) <http://www.iqnomy.com/downloads/cases/IQNOMY_liquid_e-mail_marketing_cases.pdf>`_

Tutorial
--------

.. code-block:: html

 <b>Visitor</b>
 <br />
 <table class="mytable">
 	<tr>
 		<td>Visitor</td>
 		<td>$visitor.id</id>
 	</tr>
 	<tr>
 		<td>Sessions</td>
 		<td>$visitor.sessionCount</td>
 	</tr>
 	<tr>
 		<td>Since</td>
 		<td>$visitor.dateCreated</td>
 	</tr>
 	<tr>
 		<td>ExternalId</td>
 		<td>$visitor.externalId</td>
 	</tr>
 	<tr>
 		<td>Engagescore</td>
 		<td>$session.value</td>
 	</tr>
 </table>
        #set($dimensions=$properties["dimensions"])
 <b>Dimensions: $dimensions.size()</b>
 <table class="mytable">
 	<col span="2" style="font-style: italic" />
 	#foreach( $profileProperty in $dimensions)
 	<tr>
 		<td>$profileProperty.dimension.name</td>
 		<td>$profileProperty.label</td>
 	</tr>
 	#end
 </table>
 <b>Soft profile</b>
 <br />
 #set($softProfile = $service.getSoftProfile($visitor))
 <div id="wordcloud"
 	style="border: 1px solid #f00; height: 150px; width: 150px;">
 	#foreach( $word in $softProfile.words)
 		#set( $weight =$word.weight * 100)
 		<span data-weight="$weight">$word.value</span>
 	#end
 </div>
 
 <b>Visitor properties:</b>
 <table class="mytable">
 	<col span="2" style="font-style: italic" />
 	#set($visitorProperties=$service.getVisitorProperties($visitor))
 	#if($visitorProperties)
 		#set($vpEntrySet =
 		$visitorProperties.entrySet()) #foreach( $vpEntry in $vpEntrySet)
 		<tr>
 			<td>$vpEntry.getKey()</td>
 			<td>$vpEntry.getValue()</td>
 		</tr>
 		#end
 	#end
 </table>
 
 <b>Session properties:</b>
 <table class="mytable">
 	<col span="2" style="font-style: italic" />
 	#set($sessionProperties=$service.getSessionProperties($session))
 	#if($sessionProperties) #set($spEntrySet =
 		$sessionProperties.entrySet()) 
                 #foreach( $spEntry in $spEntrySet)
 			#if(!$spEntry.getKey().equals("fp") && !$spEntry.getKey().equals("ip4") && !$spEntry.getKey().equals("ip6"))
      	  	     <tr>
 			    <td>$spEntry.getKey()</td>
 			   <td>$spEntry.getValue()</td>
 		    </tr>
                   #end
 		#end
 	#end
 </table>

Other tutorial
--------------

.. code-block:: html

 #set($softProfile = $service.getSoftProfile($visitor))

 
 <div class="main-field" style="background-color: rgb(239, 239, 239); height:510px; width:223px; position:relative; margin-left:0px; margin-top:0px; padding-left:10px; padding-right:10px; padding-top:10px; float:left; border: 1px solid #929292;">
 <div id="pr-top">
 <img src="http://iqnomy.com/iq-demo/visitor-profile/images/user-icon-small.png" style="position:relative; margin-left:0px; float:left;"/>
 
 <div id="pr-title" style="position:relative; left:10px; float:left;">
 YOU</div>
 
 <div class="pr-id" style="position:relative; right:0px; float:right;">$visitor.id</div>
 
 </div>
 <img src="http://iqnomy.com/iq-demo/visitor-profile/images/arrow-small.png"style="position:absolute; margin-top:20px; float:left; left:20px;"/>
 
 <br/>
 
 <table class="pr-table" style="margin-top:20px; font-size:12px;">
 	<tr>
 		<td class="pr-first1">Sessions</td>
 		<td class="pr-second1">$visitor.sessionCount</td>
 	</tr>
 	<tr>
 		<td class="pr-first1">tracked since</td>
 		<td class="pr-second1">$visitor.dateCreated</td>
 	</tr>
 	<tr>
 		<td class="pr-first1">EngageScore</td>
 		<td class="pr-second1">$session.value</td>
 	</tr>
 </table>
 <br/>
 <!--
 <b>Soft profile</b>
 <div id="wordcloud" style="border: 1px solid #791456; background-color:#fff; margin-top:5px; height: 85px; width: 220px;">
 	#foreach( $word in $softProfile.words)
 		#set( $weight =$word.weight * 100)
 		<span data-weight="$weight">$word.value</span>
 	#end
 </div>
 <br/>
 -->
 <div class="container">
 #set($dimensions=$properties["dimensions"])
 
 			<section class="ac-container">
 				<div>
 					<input id="ac-1" name="accordion-1" type="radio" checked />
 					<label for="ac-1">Visitor interests <h3>$dimensions.size()</h3></label>
                   <article class="ac-small">
 					<table class="mytable">
 	<col span="2" style="font-style: italic" />
 	#foreach( $profileProperty in $dimensions)
 	<tr>
 		<td class="pr-first">$profileProperty.dimension.name</td>
 		<td class="pr-second">$profileProperty.label</td>
 	</tr>
 	#end
 </table>
 					</article>
 				</div>
 				<div>
 					<input id="ac-2" name="accordion-1" type="radio" />
 					<label for="ac-2">Visitor data</label>
 					<article class="ac-small">
 						<table class="mytable">
 	<col span="2" style="font-style: italic" />
 	#set($visitorProperties=$service.getVisitorProperties($visitor))
 	#if($visitorProperties)
 		#set($vpEntrySet =
 		$visitorProperties.entrySet()) #foreach( $vpEntry in $vpEntrySet)
 		<tr>
 			<td class="pr-first">$vpEntry.getKey()</td>
 			<td class="pr-second">$vpEntry.getValue()</td>
 		</tr>
 		#end
 	#end
 </table>
 					</article>
 				</div>
 				<div>
 					<input id="ac-3" name="accordion-1" type="radio" />
 					<label for="ac-3">Session data</label>
 					<article class="ac-small">
 						<table class="mytable">
 	<col span="2" style="font-style: italic" />
 	#set($sessionProperties=$service.getSessionProperties($session))
 	#if($sessionProperties) #set($spEntrySet =
 		$sessionProperties.entrySet())
 		#foreach( $spEntry in $spEntrySet)
 			#if(!$spEntry.getKey().equals("fp") && !$spEntry.getKey().equals("ip4") && !$spEntry.getKey().equals("ip6"))
 			<tr>
 				<td class="pr-first">$spEntry.getKey()</td>
 				<td class="pr-second">$spEntry.getValue()</td>
 			</tr>
 			#end
 		#end
 	#end
 </table>
 					</article>
 				</div>
 			</section>
         </div>
         </div>
         <a id="_iqboxctn18btn" class="_iqboxcnt18btn" href=" " style="position:relative; float:left; margin-left:0px; width:38px; height:45px;"><img src="http://iqnomy.com/iq-demo/visitor-profile/images/rounded-button-purple-big.png" style="height:45px; width:38px; z-index:999999; "/></a>
         
         
         
         
         
         
         
         
         
         
         
 <style>
 .ac-container{
 	width: 220px;
 	margin: 10px auto 30px auto;
 	text-align: left;
 }
 .ac-container label{
 	font-family: arial, 'Arial Narrow', Arial, sans-serif;
 	padding: 3px 30px;
 	position: relative;
 	z-index: 20;
 	display: block;
 	height: 24px;
 	cursor: pointer;
 	color: #fff;
 	line-height: 24px;
 	font-size: 14px;
 	background-image: url(http://iqnomy.com/iq-demo/visitor-profile/images/purple-header-bg.jpg);
 	
 	filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffffff', endColorstr='#eaeaea',GradientType=0 );
 	box-shadow: 
 		0px 0px 0px 1px rgba(155,155,155,0.3), 
 		1px 0px 0px 0px rgba(255,255,255,0.9) inset, 
 		0px 2px 2px rgba(0,0,0,0.1);
 }
 
 .ac-container label h3{
 	font-size:14px;
 	color:#ffb412;
 	right:15px;
 	position:absolute;
 	top:-10px;
 	height:5px;
 	width:5px;
 }
 .ac-container label:hover{
 	background: #9c2874;
 }
 .ac-container input:checked + label,
 .ac-container input:checked + label:hover{
 background-image: url(http://iqnomy.com/iq-demo/visitor-profile/images/purple-header-bg.jpg);	color: #fff;
 	box-shadow: 
 		0px 0px 0px 1px rgba(155,155,155,0.3), 
 		0px 2px 2px rgba(0,0,0,0.1);
 }
 .ac-container label:hover:after,
 .ac-container input:checked + label:after{
 	content: '';
 	position: absolute;
 	width: 24px;
 	height: 24px;
 	left: 3px;
 	top: 2px;
 	background: transparent url(http://iqnomy.com/iq-demo/visitor-profile/images/arrow-down.png) no-repeat center center;	
 }
 .ac-container input:checked + label:after{
 	background-image: url(http://iqnomy.com/iq-demo/visitor-profile/images/arrow-right.png);
 	display:yes;
 }
 .ac-container input{
 	display: none;
 }
 .ac-container article{
 	background: rgba(255, 255, 255, 0.5);
 	margin-top: -1px;
 	overflow: hidden;
 	height: 0px;
 	position: relative;
 	z-index: 10;
 	-webkit-transition: height 0.3s ease-in-out, box-shadow 0.6s linear;
 	-moz-transition: height 0.3s ease-in-out, box-shadow 0.6s linear;
 	-o-transition: height 0.3s ease-in-out, box-shadow 0.6s linear;
 	-ms-transition: height 0.3s ease-in-out, box-shadow 0.6s linear;
 	transition: height 0.3s ease-in-out, box-shadow 0.6s linear;
 }
 .ac-container article p{
 	font-style: italic;
 	color: #777;
 	line-height: 23px;
 	font-size: 14px;
 	padding: 20px;
 	text-shadow: 1px 1px 1px rgba(255,255,255,0.8);
 }
 .ac-container input:checked ~ article{
 	-webkit-transition: height 0.5s ease-in-out, box-shadow 0.1s linear;
 	-moz-transition: height 0.5s ease-in-out, box-shadow 0.1s linear;
 	-o-transition: height 0.5s ease-in-out, box-shadow 0.1s linear;
 	-ms-transition: height 0.5s ease-in-out, box-shadow 0.1s linear;
 	transition: height 0.5s ease-in-out, box-shadow 0.1s linear;
 	box-shadow: 0px 0px 0px 1px rgba(155,155,155,0.3);
 }
 .ac-container input:checked ~ article.ac-small{
 	height: 140px;
 	padding-top:5px;
 	padding-left:5px;
 }
 .ac-container input:checked ~ article.ac-medium{
 	height: 180px;
 }
 .ac-container input:checked ~ article.ac-large{
 	height: 230px;
 }
 .pr-first1{
 	font-size:12px;
 	color:#757575;
 	text-decoration:underline;
 }
 .pr-second1{
 	font-size:12px;
 	color:#757575;
 	color:#098826;
 	padding-left:10px;
 }
 .pr-first{
 	font-size:12px;
 	color:#757575;
 	text-decoration:underline;
 }
 .pr-second{
 	font-size:12px;
 	color:#757575;
 	color:#098826;
 	padding-left:25px;
 }
 .pr-title{
 	font-size:16px;
 	color:#575757;
 	font-weight:bold;
 
 }
 .pr-id{
 	font-size: 14px;
 	color:#791456;
 }
 </style>

.. _events:

##########
Event data
##########

****************************************
Connect data with a profile
****************************************

Input of data into a profile can be used from all connected channels.

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

There are 4 ways to add data to the profile:

#. :ref:`API <api>`

With the :ref:`User the websitescript <websitescript>`

#. Page-load
#. TrackEvent
#. URL parameters

