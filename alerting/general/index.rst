Alerting General Information
============================

Overview
^^^^^^^^
The alerting feature of anyblock.tools is capable of monitoring and alerting mostly all of the information that a blockchain emits.

If you haven't checked yet, or just came here for the first time, you might `contact us <mailto:contact@anyblockanalytics.com>`__
to get access to the alerting feature.

Make sure you can access the alerting feature by opening the `Dashboard <https://account.anyblock.tools/alerting/dashboard/>`__.
You should see an (empty) list of alerting rules.

Frontend Usage
^^^^^^^^^^^^^^
Just hit `+ New` on the `Dashboard page <https://account.anyblock.tools/alerting/dashboard/>`__ to add a new alerting rule.
Give it a name, select the network and configure when your data is considered *final*.
See the [Example section](#examples) for the actual configuration.


API Usage
^^^^^^^^^
You can access the API with cURL or your preferred REST library. See `the documentation <../endpoints>`__ for authorization details.

Properties
^^^^^^^^^^
After you visit the dashboard you might see an empty list, you should create one first.

Name
""""
The name has just visible purpose.

Counter
"""""""
An alert has a counter which shows how often an alert has been triggered since its creation. The counter is visible in the list overview.

Network
"""""""
An alert is always linked to a specific network which can be chosen from the dropdown.

Confirmation Count
""""""""""""""""""
The block distance needed to trigger this alert. Using ``0`` means that it will triggered directly without waiting for a new block to confirm. 
Be aware that a **reorg** on the blockchain might happen and thus the alert will trigger false-positive results - you should wait at least ``5`` blocks to be on the safe side.

Send Pending Alerts
"""""""""""""""""""
If the confirmation count is not reached, you may allow this alert to send matches though. Every Block will then trigger a new pending match.

JSON Configuration
""""""""""""""""""
The definition of an alert is currently checked against a `JSON schema <https://json-schema.org/>`__ in the background (and also before you save it).
You can find help and the actual alerting schema :doc:`here <../schema/index>`.
