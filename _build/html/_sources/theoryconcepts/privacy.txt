.. _privacy:

#######
Privacy
#######

In order to follow the anonymous visitors of a website, page visits are being tracked.

By implementing the IQNOMY script, each visitor visiting a page of the website will automatically be allocated a unique identification number. The identification number is stored in a cookie within the visitor’s computer. This cookie contains two numbers: the script id and the visitor id. In this way, returning visitors can be identified based on this cookie (if not being deleted by the visitor).  

When a page is being visited, the IQNOMY script sends along some data:  the URL referrer of the website that was visited before the user clicked on the actual page and the URL of the current page. IQNOMY prepares a session id for every visit that the visitor brings on the website. In this way, IQNOMY can recognize that an anonymous visitor with an identification number has visited the website several times. IQNOMY analyzes the URL of the page that is being visited. Basically, this is the same URL that can be seen by the visitor in the browser.

IQNOMY now knows:
*the visitor id
*the visitor session id
*referrer page
*url of the visited page
*date / time

If the website designers do not show any privacy sensitive information in the URL, then these will not be passed on to IQNOMY. Besides this, an [[Security|SSL connection]] can be set up with IQNOMY, which enables data encryption of the visitors being followed.
