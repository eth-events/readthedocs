Alerting General Information
============================

Overview
^^^^^^^^
The alerting feature of eth.events is capable of monitoring and alerting mostly all of the information that a blockchain emits.

If you haven't checked yet, or just came here for the first time, you might `contact us <mailto:contact@eth.events>`__
to get access to the alerting feature.
In any other case you might already have access - then you should visit the `alerting dashboard <https://account.eth.events/alerting/dashboard/>`__.

Here you can create, delete and edit alerts.

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

JSON Configuration
""""""""""""""""""
The definition of an alert is currently checked against a `JSON schema <https://json-schema.org/>`__ in the background (and also before you save it).
You can find help and the actual alerting schema :doc:`here <../schema/index>`.
