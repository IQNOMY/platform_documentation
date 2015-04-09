###
FAQ

.. contents::

=English FAQ's=
==How to track visitors?==
You can track visitors using different techniques. The most common way to identify a visitor is to use a cookie. More information about tracking visitors can be found at [[Tracking integration with website]]

==What's the realtimedesk?==
The realtimedesk shows you realtime analysis of visitors using your website. By analysis your visitors we can see what their interests are, type of visitor, etc. With this information you can actually see what visitors want.

==How many visitors can IQNOMY handle?==
The IQNOMY platform can handle enormous amounts of data. For existing customers using the platform we provide uptime by working redundant and clustered. Our technical infrastructure is scalable and working with the newest techniques to make this possible.

==How is IQNOMY able to analyse visitors?==
That's the knowledge of IQNOMY. Years we developed and research these techniques. What makes use different from companies that track visitors is that we actually know what visitors read. Language technology and Selflearning technologies are key for our applications.

==Is tracking really anonymous?==
Yes, we don't know who the visitor is. We can only identify a visitor for '''one''' MyLiquidSuite. Therefor we can't share this data over more MyLiquidSuites. Read more: [[Anonymous visitors and privacy]]
==Is visitor privacy respected?==
Yes, Read more: [[Anonymous visitors and privacy]]

==What do you mean by <BODY> in your script description?==
The email you receive after registering your MyLiquidSuite gives you a short description of the implementation of the script and the script itself. The script can be put on your website by a webmaster. Send the email your received to your webmaster or the company that designed your website.[[Script implementation tutorials]] show you several implementations of the script on websites. If you still have problems implementing the script on your website contact us [mailto:support@iqnomy.com support@iqnomy.com].

==How to start your MyLiquidSuite?==

[http://www.slideshare.net/iqnomy/iqnomy-how-to-start-your-liquid-suite-part-1 How to start your MyLiquidSuite]

=Nederlandse FAQ's=
==Wat is de laadtijd van de code?==
Gemiddeld tussen de 0 en 1 seconde. IQNOMY houdt de reactietijd van alle tracks bij via de logs. Zo kan bij een vermindering van de reactietijd gereageerd worden door infrastructure upgrade of softwareaanpassingen. Overigens is de aanroep van het script asynchroon, waardoor de bezoeker hier niks van merkt. Daarnaast worden voor iedere versie performance en stabiliteitstesten uitgevoerd. Deze twee punten zijn basiseisen van de applicatie, waarbij we constant bezig zijn deze te optimaliseren.

==Welke ervaringen hebben jullie voor het bereiken van de best mogelijke performance? Hoe zit de techniek hierachter in elkaar?==
De techniek erachter is moeilijk uit te leggen, omdat verschillende functies in de applicatie verschillende optimale oplossingen betreffen. Dit alles draagt bij aan performance en stabiliteit. We gebruiken verschillende domeinen om op deze manier de hoeveelheid geheugen te kunnen optimaliseren. Daarnaast zijn de technieken loadbalanced en clustered uitgevoerd en worden alleen de zaken die realtime uitgevoerd moeten worden direct uitgevoerd. Zowel in de softwarearchitectuur als in de infrastructuur is hier rekening mee gehouden. Daarnaast wordt er voor de data gebruik gemaakt van indexen, databases Master- slave uitvoeringen en No-SQL db’s voor grote hoeveelheden data. Daarnaast wordt ETL toegepast om de data te aggregeren naar uren, dagen, maanden. Zo blijven de realtime queries beperkt. Natuurlijk wordt er ook opgelet dat data in cache blijft staan als deze vaak gebruikt wordt.

==Is er een oplossing gelijk waarbij voor pagina’s zonder in-content targeting de code later geladen wordt?==
De oplossing kan op verschillende manieren geimplementeerd worden. Zowel serverside als clientsite. We zullen de juiste technische oplossing voor deze implementatie met de ict afdeling van afstemmen. Overigens kan tracking van de bezoeker ook worden ingesteld bij de aanroep van in-content targeting, hierdoor kan het losse tracken later worden uitgevoerd. Op de pagina’s waar geen in-content targeting wordt gebruikt is dan de realtime laatste data minder relevant.

==Andere mogelijke oplossingen (bijvoorbeeld server-side: implicaties voor implementatie)==
Ja, requests zijn er nog nodig ivm het uitrekenen van profielen en het adviseren van de content.

De oplossing voor het tonen van in-content targeting kan op verschillende niveaus plaatsvinden. Als er voor wordt gekozen dat het CMS zaken overruled hoeven er in dat geval natuurlijk geen requests naar IQNOMY worden gestuurd.

==Is de te variëren content direct zonder tussenkomst van Iqnomy door ons te wijzigen?==
Ja, je kunt ook meerdere mensen uitnodigen met een reporter of administrator rol. SaaS opzet

==Kunnen we zelf direct nieuwe experimenten opzetten zonder tussenkomst van Iqnomy?==
Ja, er is ook veel online documentatie aanwezig die steeds meer uitgebreid wordt.

==Is er een mogelijkheid om zonder javascript te werken voor het plaatsen van nieuwe containers?==
Vaak hebben bedrijven IT nodig voor het plaatsen van Javascript. Veel CMS'en zoals bijv. Tridion of Sharepoint bieden de mogelijkheid een widget te ontwikkelen. Per geplaatste widget kun je dan een containernr opgeven, zodat je bij een uitbreiding van Liquid Internet op je website geen ict aanpassingen hoeft te doen.

==Kunnen we zelf regels instellen die het automatische algoritme ‘overrulen’?==
Ja, in iqnomy, maar sommige klanten kiezen ervoor om in het CMS IQNOMY te overrulen. Naast het automatisch algoritme zijn er ook andere technieken die er in IQNOMY worden toegepast. Je kunt experimenteren met deze technieken door bij een bepaald percentage van de bezoekers een andere techniek te gebruiken. Je kunt zo meerdere technieken tegelijk testen. Het percentage 100% kan verdeeld worden over alle technieken.

Per techniek wordt bijgehouden wat het resultaat is en welke bezoeker welke techniek op welk moment heeft gezien. Veel data dus, maar dit wordt weer gebruikt voor de analyses.

==Kunnen we zelf regels instellen?==
''Voor bijvoorbeeld bezoekers die specifieke pagina’s hebben bezocht, of bezoekers die via een specifieke campagne (url parameter) of zoekwoord (referrer) binnenkomen, ingelogde bezoekers, etc.''

Ja, wel opletten met privacy van ingelogde bezoekers. Je kunt deze technische namelijk blijven volgen met de inlognaam buiten het inloggedeelte.

Zoekwoorden uit referrers of de search op de site kunnen ook worden gebruikt. Je kunt zo ook personal search toepassen.

==Hoe maken we alles meetbaar in SiteCatalyst?==
''Kan een standaard tagging hierin voorzien, zonder dat er later aanpassingen nodig zijn voor specifieke experimenten?''
IQNOMY maakt standaard gebruik van de standaard tagging lqiid. Hoe standaard wil je deze hebben? Bijv. IQNOMY moet altijd automatisch iets toevoegen. Je wilt zelf een standaard toevoeging per situatie kunnen doen. De tagging standaard, maar met handmatig in te vullen id’s?

==Inloggen in management lukt niet==
Als het inloggen in de beheermodule van het IQNOMY platform niet lukt dan kan het zijn dat de beveiliging van de browser dit tegenhoudt. Voor daarom de loginpagina van IQNOMY in als vertrouwde site.
###
