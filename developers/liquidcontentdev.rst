
Het is mogelijk om custom javascript-code toe te voegen aan een liquid content. Deze code wordt uitgevoerd op het moment dat de liquid content getoond wordt.
 
In de template van de liquid content dien je je custom javascript-code te plaatsen in een script-tag geïdentificeerd met "_iqnomy_extrascript". Voorbeeld:
 
 <script type="text/javascript" id="_iqnomy_extrascript">
   alert('custom code');
 </script>
 
Hieronder verschillende manieren om dit te implementeren.
 
=Toepassing 1:=
 
- minder goed onderhoudbaar als custom script in meerdere liquid contents nodig is
- geen aanpassing aan container-pagina's nodig
 
In liquid content plaatsen:
 
 <script type="text/javascript" id="_iqnomy_extrascript">
   alert('custom code');
 </script>
 
=Toepassing 2a:=
 
- beter onderhoudbaar als custom script in meerdere liquid contents nodig is
- wel aanpassing aan container-pagina's nodig
- minder goed onderhoudbaar als custom script op meerdere pagina's nodig is.
 
In liquid content plaatsen:
<script type="text/javascript" id="_iqnomy_extrascript">
myFunction('custom code');
</script>
 
In container-pagina plaatsen:
  
 <script type="text/javascript">
   function myFunction(str) {
     alert(str);
   }
 </script>
 
 
=Toepassing 2b:=
 
- beter onderhoudbaar als custom script in meerdere liquid contents nodig is
- wel aanpassing aan container-pagina's nodig
- beter onderhoudbaar als custom script op meerdere pagina's nodig is
- javascript include-bestand dient beschikbaar te zijn op de website
 
 <script type="text/javascript" id="_iqnomy_extrascript">
   myFunction('custom code');
 </script>
 
In container-pagina plaatsen:
 
 <script type="text/javascript" src="/my-include.js">
 </script>
 
In /my-include.js plaatsen:
 
 function myFunction(str) { 
   alert(str);
 }

=See also=
*[[Omniture|Omniture tracking van Liquid Content]]
*[[Layout Liquid Content]]

========
Omniture
========

Omniture sitecatalist is used as an analytics tool for websites. To be able to track the IQNOMY liquid content you can integrate the Omniture script with the IQNOMY script.

=Content of variables Omniture=
First you have to decide what the content is of the variables are using to track in Omniture.
			
*var s_account='accountname';
*s.pageName = 'Companyname | Pagename | IQNOMY Personalization';
*s.channel = 'Companyname consumers';
*s.prop43=selectorType;

[[Matching methods|Selector types]] are put in the 's.prop43'. Probably this is a variable that is available in Omniture. Just ask an Omniture expert and [[#Example of Omniturescript with IQNOMY container script|see implementation example below]]. The variable s.prop43 is used there.

=Containerscript with Omniture code=
In IQNOMY you can get the [[container script]]. This script can be used together with an adjusted Omniturescript. The container script is used to make the content liquid. With every liquid impression the Omniture script is also filled and send. 

See example below [[#Example of Omniturescript with IQNOMY container script]]

=HTML of the Liquid content=
In the liquid content you can put extra information that is used by the Omniture script. First the selector types and second the bnr code. With this code the view and the click of the content can be tracked by Omniture. [[#Example of HTML from Liquid content|See example below]]

[[Layout_Liquid_Content#Using_standard_layouts|Other examples]] of html in the liquid content.

=Examples=
==Example of Omniturescript with IQNOMY container script==
 <nowiki><!--IQNOMY-->					

 <div id='Omniture_hidden' style='display:none'>
	<!-- Begin Omniture -->
	<!-- SiteCatalyst code version: H.2.
	Copyright 1997-2005 Omniture, Inc. More info available at
	http://www.omniture.com -->
	<script language="JavaScript" src="domain/example/_administration/include/omniture.js"></script>
	<script language="JavaScript">
	var iqImpr = 0;
	function iqImpressed(selectorType) {
		if (++iqImpr > 1)
			return;	
			
		var s_account='accountname';
		s.pageName = 'Companyname | Pagename | IQNOMY Personalisatie';
		s.channel = 'Companyname consumers';
		s.prop43=selectorType;

		s.eVar43=s.prop43;


		/************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
		var s_code=s.t();if(s_code)document.write(s_code)
	}//--></script>
	<script language="JavaScript"><!--
	if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
	//--></script><!--/DO NOT REMOVE/-->
	<!-- End SiteCatalyst code version: H.2. -->
	<!-- End Omniture -->
 </div>

 /*********IQNOMY container script starts from here*******/	
 <!-- add a style="width:XXXpx; height: XXXXpx"  to a div to smooth the rendering of the page -->
 <div class="column panel clear">
	<h2>Title</h2>

	<ul class="links">
		<div id="liquid_ip201">
			<div id="liquid_ip201_backup" style="display:none">
			Backup HTML
			</div>
		</div>
	</ul>
		
	<script type="text/javascript">
		var loadState_liquid_ip201 = 1; 
		setTimeout("if (loadState_liquid_ip201 == 1) { loadState_liquid_ip201 = 3;      document.getElementById('liquid_ip201_backup').style.display='block'; } ", 3000);  
		var iql = document.createElement("script"); 
		iql.type = "text/javascript"; 
		iql.async = true; 
		iql.src = "//liquifier.iqnomy.com/myliquidsuite/impr2?information in script container+ escape(document.URL); 
		iql.text = "doImpression_liquid_ip201();"; 
		document.getElementsByTagName('head')[0].appendChild(iql); 
	</script>

	<!--End IQNOMY--></nowiki>

==Example of HTML from [[Liquid content]]==

In the example below you see the Omniture extra in '''Bold text'''.

<li>
<a href="$liquidContentUrl&$impressionUrlParam&'''bnr=home-$containerSelectorType$escalationCause'''" id="iqContentUrl">$liquidContentName</a>

</li>

'''<script type="text/javascript" id="_iqnomy_extrascript"> iqImpressed('$containerSelectorType$escalationCause'); </script>'''

==Example of Omniture report==
Periode	date-2012 t/m date-2012

{|border='1'	
|-
|
|Home	
|-
|Visits op de pagina	
|631.865

|-
|Visits op 'Fixed'
|406.612	 

|-
|Visits op 'DIMENSIONCLASSIFICATIONNO_RESULT'
|128.677	 

|-
|Visits op 'DIMENSIONCLASSIFICATION'
|82.042	 

|-
|Visits op 'Random'
|39.091	 

|-
|
|	 

|-
|Kliks op 'Fixed'
|3.283	 

|-
|Kliks op 'DimensionclassificationNo_Result'
|902		 

|-
|Kliks op 'Dimensionclassification'
|884	 

|-
|Kliks op 'Random'
|823	  

|-
|
|	 

|-
|Klikratio 'Fixed'
|0,8%	 

|-
|Klikratio 'DimensionclassificationNo_Result'
|0,7%	 

|-
|Klikratio 'Dimensionclassification'
|1,1%	 

|-
|Klikratio 'Random'
|2,1%	 

|-
|
|	 

|-
|Exitrate 'Fixed'
|17,4%	 

|-
|Exitrate 'DimensionclassificationNo_Result'
|18,1%	 

|-
|Exitrate 'Dimensionclassification'
|17,1%	 

|-
|Exitrate 'Random'
|18,1%	 

|-
|
|	 

|-
|Pagina's per bezoek 'Fixed'
|7,5	 

|-
|Pagina's per bezoek 'DimensionclassificationNo_Result'
|7,1	 

|-
|Pagina's per bezoek 'Dimensionclassification'
|9,0	 

|-
|Pagina's per bezoek 'Random'
|7,8	 

|}

=See also=
*[[Use javascript in Liquid Content]]
*[[Layout Liquid Content]]


=====================
Layout liquid content
=====================

=Using standard layouts=
A liquid content can be presented in any way you like. If your CMS does the presentation the liquid content will 'advise' your CMS to present eg. id 1300.

You can also use the HTML template to present the Liquid content. In this HTML template you can use different code's to reuse the liquid content data

*$liquidContentUrl : the link URL will be used.
*$impressionUrlParam : the platform will add an unique lqiid (liquid id) to the URL. This way the MLS can track a click on the link. 
*$liquidContentName : the title of the liquid content is used.
*$liquidContentDescription : the liquid content description is used.
*$containerSelectorType$escalationCause: This will show the way the liquid content was selected. You can use this variable to track this in analytics tools.

If you want to use javascript in your html template [[Use javascript in Liquid Content|Read more]]

=HTML template tutorials=
==Tutorial Basic==
 <nowiki><a href="$liquidContentUrl&$impressionUrlParam" id="iqContentUrl">$liquidContentName</a><br> </nowiki>

==Tutorial 2==
 <nowiki><section class="box topic-spotlight">
	<header>
		<h1>Relevant blog</h1>
	</header>
 <div class="body">
	<article class="clickable"> 
		<header>
			<h1><a href="$liquidContentUrl&$impressionUrlParam" id="iqContentUrl">$liquidContentName</a></h1>
		</header>
		<div class="body">
				<p class="content" id="iqContentDescription">
					$liquidContentDescription
				</p>
		<a class="button" href="$liquidContentUrl&$impressionUrlParam" id="iqContentUrl" style="color: #FFFFFF;">read more</a>
		</div>
	</article>
	<div class="more"><a href="http://www.iqnomy.com/blog/categorie/site-owners/"><span>All blogs</span></a>
 </div>
 </section>

 <script type="text/javascript" id="_iqnomy_extrascript">
	document.getElementById('iqContentUrl').href=document.getElementById('iqContentUrl').href.replace("//automatiseringgids.inict.nl", "//www.automatiseringgids.nl");
	var workStr = document.getElementById('iqContentDescription').innerHTML;
	var maxLen = 150;
	if (workStr.length > maxLen) {
		workStr = workStr.substr(0, maxLen);
		workStr = workStr + "...";
		document.getElementById('iqContentDescription').innerHTML = workStr;
	}
 </script>
</nowiki>

==Tutorial 3==
URL list together with javascript to trigger [[Omniture]].

 <nowiki>
 <li>
  <a href="$liquidContentUrl?$impressionUrlParam&bnr=home-$containerSelectorType" id="iqContentUrl">$liquidContentName</a>
 </li>
 <script type="text/javascript" id="_iqnomy_extrascript">
   iqImpressed('$containerSelectorType');
 </script></nowiki>

=See also=
*[[Omniture|Omniture tracking of Liquid Content]]
*[[Use javascript in Liquid Content]]
