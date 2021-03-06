Alerting JSON Schema
=====================

The schema has three main parts:

- ``targetType``
- ``targetMap``
- ``alerts``

The ``targetType`` is the type of entity that our alerting infrastructure will look for and then match against your configured ``targetMap``.
The ``alerts`` define types of actions that should get triggered once an entity has been matched.

Target-Type
^^^^^^^^^^^
The target-type can be any that is defined in the enumeration of this element. In that case it is currently list as:

- ``Block``
- ``Event``
- ``Log``
- ``Transaction``
- ``Call``
- ``Trace``
- ``Balance``
- ``Input``
- ``Output``
- ``Method``
- ``Contract``

(Omitted other types as they are not user-relevant)

Target-Map
^^^^^^^^^^
The ``targetMap`` defines an array of target-definitions that the entity should have in order to be a successful match and trigger an alert.
Each of the target-definition can have:

- ``name``
- ``value``
- ``operator``
- ``operatorParameters``
- ``useScaledValue``

Name
""""
The name of the attribute that should be inspected 

Example: ``address`` for a log to inspect the contract address of a log that came through)

In order to decide which fields are available you should look at our :doc:`Elastic Data-Structure <../../elastic/data-structure/index>`.

Value
"""""
The value the attribute should have represented as a String, or String-Array in case you  want to match one of multiple values 

Example: ``0xe3818504c1B32bF1557b16C238B2E01Fd3149C17`` for a contract address

Operator
""""""""
The operator that should be used to match the ``value`` against:

- ``Greater``: **>** ``value``
- ``Greater or Equal``: **>=** ``value``
- ``Less``: **<** ``value``
- ``Less or Equal``: **<=** ``value``
- ``Equals``: **==** ``value`` (For String *AND* Numeric)
- ``Equals (ignore case)``: Case insensitive variant of ``Equals``
- ``Equals any``: Matches any against ``value`` using ``Equals`` - in that case ``value`` must be a String-Array
- ``Equals any (ignore case)``: Case insensitive variant of ``Equals any``
- ``Inspect``: Steps into that property

Operator: Inspect
"""""""""""""""""
Some of the Target-Types have a deep structure. For example ``call`` and ``event`` both have the property ``args`` which contain the
arguments of an Eth-Transaction (call) and the parameters of an emitted Eth-Log.

In order to inspect the arguments/parameters, we need the ``Inspect`` operator.

The stepping works 2 levels deep (Eth-Traces have a structure 2 levels deep).

Usage of Scaled values
""""""""""""""""""""""
In case of ``call`` and ``event`` and their arguments/parameters you are able to match them against the scaled variant of them.
This special flag is only available on the 2nd level of ``Inspect`` because the scaled values only appear there. 

**Note**: We can only decode values if the event/call comes from a popular token where we have the number of decimals used.

Alerts
^^^^^^
The ``alerts`` property defines an array with alert-definitions that should get triggered once a match was found.
Each of the alert-definition can have:

- ``type``
- ``parameters``
- ``payload``

Type
""""
The type defines the type of the alert which can be:
- ``Webhook (GET)``: Calls an endpoint using *HTTP/GET*
- ``Webhook (POST)``: Calls an endpoint using *HTTP/POST* with the body encoded in JSON
- ``Email``: Will send an email 
- ``Slack``: Triggers a slack webhook URL

Parameters
""""""""""
This object type property of the schema depends on the type you have chosen.

* ``Email``: 
  * ``recipients`` (String-Array) with email-addresses that should get the alerting-mail
* ``Slack``: 
  * ``url`` (String) The full URL of the webhook (can be generated by a Slack-Adminstrator)
  * ``text`` (String) Introductional text (slack emoticons can be used, like `:warning:`
  * ``channel`` (String) The channel where to post the alert
  * ``username`` (String) The username that the message should be posted as
* ``Webhook (GET)``: 
  * ``url`` (String) The url that should get called
* ``Webhook (POST)``: 
  * ``url`` (String) The url that should get called

**Note**: Strings like ``{transactionHash}`` inside of the webhook URLs will get replaced with the actual value given from the payload.

Payload
"""""""
A array of objects that should get send with the alert, along the matching properties defined in the ``targetMap``.
Each of them can have the following (the syntax is almost the same to the ``operator``:

- ``fieldType``: Can be ``Field`` or ``Sub Field``
- ``fieldName``: The name of the property that should get extracted from the matching entity and send along with the alert
- ``subPayloads``: If ``Sub Field`` is chosen, you can append another level of inspection

Schema JSON
^^^^^^^^^^^
The current alerting schema formatted as a `JSON schema <https://json-schema.org/>`__:

.. literalinclude:: ./schema.json
   :language: json