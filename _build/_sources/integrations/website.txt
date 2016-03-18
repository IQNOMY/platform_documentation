#######
Website
#######

To integrate your website with IQNOMY you can use the standard IQNOMY
websitescript. You will receive the script if you create a liquid account. The
script has two main functionalities:

* Tracking website visitors
* Integrate Liquid Internet

The standard tracking functionality is to track the website URL. 

.. seealso::
  :ref:`Customize the script <websitescript>`

************************
Tracking Code Quickstart
************************

The basic functionality of the script is tracking your website visitor.

The basic script should be on every website page

.. code-block:: javascript

   <script>
    var _iqnomytenant = XXXXXXXXX;
    var _iqnomyImpress = { hostAndPort: "tracker.iqnomy.com", timeout: 5000 };
    (function() {
    var _iqs = document.createElement('script'); _iqs.type = 'text/javascript'; _iqs.async = true;
    _iqs.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'static.iqnomy.com/myliquidsuite/js/IQImpressor.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(_iqs, s);
    })();
   </script>

.. note::
   On the XXXXXXX should be your unique Liquid Account id.

Using the script for Liquid Internet
====================================

*******************
Personalize website
*******************

The websitescript can be used for personalization of your website. You can use the script for personalization with liquid internet without doing any other integration with your website code. By defining a container in IQNOMY you can inject HTML from a liquid content into your webpages.

Implement an empty div
======================
.. figure:: _static/images/adddiv1.png

'''Another option'''
If you are not sure about the div design you can contact your IT team or us.

.. figure:: _static/images/adddiv2.png



