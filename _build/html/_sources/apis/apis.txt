.. include:: ../links

.. sidebar:: Test sidebar
   tekst 1
   test2

.. contents::

.. toctree::
   :maxdepth: 1
   index.rst

##########
How to use
##########


SOAP is not used anymore

REST
====

The REST webservices start with the link: http://management.iqnomy.com/myliquidsuite-ws/rest/dimensions/API

HTTP response format
--------------------
The REST services can response in the formats JSON or XML. The client can set this format by setting a HTTP-header Accept:

for JSON:
Accept: application/json

for XML:
Accept: application/xml

Overview REST services
----------------------

http://liquifier.iqnomy.com/myliquidsuite-ws/api



Authentication of webservices
=============================
Basic authentication is being used.

Username: ''Username''*''Account''

.. note::
 Example: christian@iqnomy.com*15854915


Webservice key: This is a random generated key. You can find this key in [[integration on own website]]

.. note::
 Example: 65565245664b7063357a533157356a6966546c494e77433645635a594878527a496f38663037554a

* Username: the emailadres you use to login to IQNOMY.
* Account: User the IQNOMY id of your environment Example 763096175
* Webservice key: API key

You can find your IQNOMY ID and Webservice key in your IQNOMY account in Discovery > Connect IQNOMY

If your infrastructure requires other security protocols please contact [mailto:support@iqnomy.com support@iqnomy.com]

########
Profiles
########
test

##########
`magento`_
##########



werkt niet :ref:`Magento <gettingstarted>`

werkt :ref:`Magento <magento:magentogettingstarted>`

werkt :ref:`magentogettingstarted`

werkt niet :rst:ref:`gettingstarted`

wert niet :py:func:`io.open`
