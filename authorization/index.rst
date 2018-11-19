Authorization
=============
To access eth.events, no matter if you just want to use the free service or have a paid service agreement, you'll need to get an API Key.

You can register for a **free** account and get an API key right now at `https://account.eth.events/ <https://account.eth.events/api/token/>`_ in just a few seconds. Go ahead, I'll wait.

Sending your API key
--------------------

Authorization Bearer Header
^^^^^^^^^^^^^^^^^^^^^^^^^^^
The fastest and most secure way to send your API key is via the *Authorization* header

.. code:: bash

  curl -X GET https://api.eth.events/status/ -H 'Authorization: Bearer $mytoken'

Basic Auth
^^^^^^^^^^
For compatibility reasons it's also possible to send the API key as your password via Basic Auth

.. code:: bash

  curl -X GET https://api.eth.events/status/ -u '$myemail:$mytoken'

Please keep in mind that you're supposed to send your **API key**, not your password here.

Query Parameter
^^^^^^^^^^^^^^^
This is by far the least secure option, because your API key may end up in all sorts of logfiles and will even be visible to network sniffers. Only use the query parameter with short lived API keys for demonstration purposes.

.. code:: bash

  curl -X GET h'ttps://api.eth.events/status/?access_token=$mytoken'

API key security
----------------
At the time of this writing there are two mechanisms in place to secure API access to your account.

Lifetime
^^^^^^^^^^^^^^^^
When creating a new API key you can select a future date at which the key will no longer work. For most applications it's obviously not reasonable to switch the API key every few days, so you can create a long lived key and keep it a secret, while you may use a key with only a few days of validity for demos and other public use cases.

Domain
^^^^^^^^^^^^^^
In case you want to use your API key in an environment where it's necessary to expose it to your intended audience (say, a website), you can additionally secure the API key with an allowed domain name. The key will then only work, if the referrer of the request matches the configured domain.

Why bother?
-----------
In the end this is a free service and anyone can get an API key anyways, so why all the hassle?

Well, for one we're going to use the API keys to restrict access to certain semi-private data, but mostly it's to control abuse to some extent.

We're monitoring the amount of requests and used data per account and in case your usage is **way** above *normal usage* we'll warn you and eventually disable your account.

In this case it would be a shame if some stranger on the internet just hijacked your API key.
