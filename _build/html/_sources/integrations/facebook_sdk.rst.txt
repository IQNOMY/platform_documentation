.. include:: ../links.rst

.. _facebook_sdk:

########
Facebook
########

IQNOMY - Facebook SDK

Send some Facebook user information automaticly to an IQNOMY hosted script that's checking the app permissions.

Code
====
You can find the SDK code at github `IQNOMY Facebook SDK`_.

Usage
=====
Three things are necessary:

#. The default IQNOMY init
#. An object `_iqfbvrs` with some user-information from facebook, you need to grab these information from your facebook connect
#. An extra script-tag that retrieves the IQNOMY Facebook script

First, load the default init of IQNOMY,

Second, set in the head of the page a new object with 3 elements:

+------------------------+----------------------------------+
| Key                    | Value description                |
+========================+==================================+
| facebookUserId         | The appname (in IQNOMY)          |
+------------------------+----------------------------------+
| facebookAccessToken    | The accestoken given by Facebook |
+------------------------+----------------------------------+

.. code-block:: javascript

	<script type="text/javascript">
	var _iqfbvrs = {
		'facebookUserId': '',
		'facebookAccessToken': ''
	};
	</script>

Third: add this small snippet of JavaScript to the head of your HTML page.

.. code-block:: javascript

	<script type="text/javascript">
	(function() {
		var _iqfbs, _iqfb = document.createElement('script'); _iqfb.type = 'text/javascript'; _iqfb.async = true;
		_iqfb.src = '//raw.githubusercontent.com/IQNOMY/facebook_sdk/master/iqnomy-fb.js?';
		_iqfbs = document.getElementsByTagName('script')[0]; _iqfbs.parentNode.insertBefore(_iqfb, _iqfbs);
	})();
	</script>

And it's done.

Every pageload, our systems checking and validate the given data.
When a user gives permissions in Facebook, the information is visible within a few moments in the IQNOMY management tool.


