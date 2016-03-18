#################
Liquid containers
#################

.. contents::

**************
Liquid content
**************

Het is mogelijk om custom javascript-code toe te voegen aan een liquid content. Deze code wordt uitgevoerd op het moment dat de liquid content getoond wordt.
 
In de template van de liquid content dien je je custom javascript-code te plaatsen in een script-tag geïdentificeerd met "_iqnomy_extrascript". Voorbeeld:

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
     alert('custom code');
   </script>
 
Hieronder verschillende manieren om dit te implementeren.
 
Toepassing 1
============
 
- minder goed onderhoudbaar als custom script in meerdere liquid contents nodig is
- geen aanpassing aan container-pagina's nodig
 
In liquid content plaatsen:

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
     alert('custom code');
   </script>
 
Toepassing 2a:
==============
 
- beter onderhoudbaar als custom script in meerdere liquid contents nodig is
- wel aanpassing aan container-pagina's nodig
- minder goed onderhoudbaar als custom script op meerdere pagina's nodig is.
 
In liquid content plaatsen:

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
   myFunction('custom code');
   </script>
 
In container-pagina plaatsen:

.. code-block:: javascript

   <script type="text/javascript">
     function myFunction(str) {
       alert(str);
     }
   </script>
 
 
Toepassing 2b:
==============
 
- beter onderhoudbaar als custom script in meerdere liquid contents nodig is
- wel aanpassing aan container-pagina's nodig
- beter onderhoudbaar als custom script op meerdere pagina's nodig is
- javascript include-bestand dient beschikbaar te zijn op de website

.. code-block:: javascript

   <script type="text/javascript" id="_iqnomy_extrascript">
     myFunction('custom code');
   </script>
 
In container-pagina plaatsen:

.. code-block:: javascript

   <script type="text/javascript" src="/my-include.js">
   </script>
 
In /my-include.js plaatsen:

.. code-block:: javascript

   function myFunction(str) {
     alert(str);
   }


*********************
Layout liquid content
*********************

Using standard layouts
======================

A liquid content can be presented in any way you like. If your CMS does the presentation the liquid content will 'advise' your CMS to present eg. id 1300.

You can also use the HTML template to present the Liquid content. In this HTML template you can use different code's to reuse the liquid content data

* $liquidContentUrl : the link URL will be used.
* $impressionUrlParam : the platform will add an unique lqiid (liquid id) to the URL. This way the MLS can track a click on the link.
* $liquidContentName : the title of the liquid content is used.
* $liquidContentDescription : the liquid content description is used.
* $containerSelectorType$escalationCause: This will show the way the liquid content was selected. You can use this variable to track this in analytics tools.

If you want to use javascript in your html template.

.. _profile-in-lc:

**********************************
Use profile data in liquid content 
**********************************

Tutorial
========

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
==============

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

