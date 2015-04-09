Every [[Creating and implementing a container|Container]] can select the [[Liquid content]] based on different matching methods. Depending on the selection method choosen while configuring the container the selector will use a method. You can choose to use for 30% one method and for 70% another. This way the diffent methods can be compaired.

.. figure:: _static/images/ContainerWorking.png

==Methods==
*'''Dimension''': If a marketeer wants to target the container you can use this technique. eg. We target 'prospect' our banner 'get invited'
*'''Semantic''': This will use the txt form the webpage and find liquid content that is similar to this page. Blogs and newssites use this technique which automaticly will find relating webpages without using tagging.
*'''Visitor classification''': Selflearning technique. IQNOMY will learn from visitor behavior and profile which liquid contents are best for this visitor. Every day this will become smarter because it uses the knowledge from all visitors to predict this visitor.
*'''Visitor semantic''': Depending on what the visitor reads IQNOMY finds out what other content is relating to this visitors interests.
*'''Random''': IQNOMY will random show content that is being used in this container. This functionality can be used to compare the results with the other techniques
*'''Fixed''': You use the IQNOMY techniques but want to know what the results would be in the situation that you were using before. We can present a percentage of your visitors with this technique so you can compare the results.

==Escalation==
If a method can't be used the fallback will start. In this escalation only the 'Random' or 'Fixed' method can be choosen.

##############
Use containers
##############
Liquid containers zijn boxen die opgenomen kunnen worden in de website of webapplicaties. Deze boxen adviseren welke content het beste getoond kan worden in de situatie waarin de communicatie met deze bezoeker zich bevindt.

De liquid containers geven advies over de content die getoond kan worden aan de bezoeker. Hiervoor worden verschillende technieken gebruikt.

    * Zelflerend
    * Push op basis van dimensies
    * Ideaal op basis van profiel bezoeker
    * Semantische relaties met content die getoond wordt aan de bezoeker
    * A-B testing
    * Vaste instellingen

Een container kan 1 of meerdere adviezen uitbrengen. Deze kunnen getoond worden op de website of door het CMS worden verwerkt om de look en feel realtime aan te passen.
Beginnende vs. geavanceerde gebruikers

Een beginnende gebruiker krijgt in 4 stappen een script beschikbaar dat gebruikt kan worden op je website om op de ideale manier te communiceren met de bezoekers van je website. De geavanceerde gebruikers kunnen instellingen doen aan de technieken op basis van statistieken instellingen veranderen of kiezen voor andere ICT oplossingen voor de integratie met de website.
Content

De content die een container adviseert staat niet in IQNOMY, maar op de website zelf. IQNOMY leest en analyseert deze content om een advies uit te kunnen brengen. De beheerders van de applicatie kunnen aangeven welke content ze door een container willen laten adviseren. Bijvoorbeeld. alle content die start met de URL http://www.iqnomy.com/blogs moet worden opgenomen in deze container. Deze container vult zich nu automatisch met nieuwe analyses van content zonder dat de beheerder hier verder naar om hoeft te kijken. Per container wordt deze analyse omgezet in liquid content. Deze liquid content zijn de content items die per liquid container geadviseerd kunnen worden.
Statistieken

Als IQNOMY voor een container een advies uitbrengt, dan krijgt dit een eigen nummer. Zo worden er dagelijks miljarden adviezen door de applicaties van IQNOMY uitgegeven. Als gebruik gemaakt wordt van de scripts van IQNOMY dan zal een container automatisch zichzelf meten. Hierdoor kan de ideale techniek worden bepaald voor een container. Bij ieder advies en iedere klik leert de container weer bij. Deze statistieken worden allemaal opgeslagen in de applicatie en geven zo per bezoeker aan wat de resultaten waren.
Integratie met de website

De makkelijkste integratie van de container met de website is het beschikbaar stellen van een stukje ruimte op de website. In de pagina of de template van de website kan een javascript van IQNOMY worden opgenomen om zo automatisch de juiste content te presenteren aan de bezoekers op de website. Voor de geavanceerdere ICT oplossingen zijn er ook mogelijkheden via webservices en staat IQNOMY ook altijd open voor eventuele andere technische mogelijkheden voor integratie met je website.
