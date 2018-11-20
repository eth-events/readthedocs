Index endpoints
===============

When interacting with the eth.events API, the base URL structure is always as follows:

/*$technology*/*$blockchain*/*$network*/*$interface*/...

The first triple of *technology*, *blockchain* and *network* describes the network you want to interact with. For most users this would be **/ethereum/ethereum/mainnet/**, which is also the default and can be omitted. Other possible values would be for example */ethereum/classic/morden/*.

The fourth part is the search interface you want to use. Currently only the ElasticSearch interface **/es/** is supported, but we're already working on SQL and GraphQL support.

So, for most users the base URL will be

.. code:: bash

  https://api.eth.events/ethereum/ethereum/mainnet/es/

ElasticSearch /es/
------------------
Following the search interface, you can select the resource you want to query. Possible values are

- `block`
- `tx`
- `log`
- `event`
- `call`

which already reflects the type parameter of the ElasticSearch query syntax.

For obvious reasons we're limiting the full scope of the ElasticSearch Query DSL, but the following APIs will work as expected:

- `search`
- `_search`
- `count`
- `_count`

It's also possible to explicitly provide the desired index in the URL which follows the format **$technology**-**$blockchain**-**$network**-**$resource**. This is completely optional but required for ElasticSearch compatibility and is normally derrived from the selected network and resource, but must match the network and resource if present.

A simple query for the latest block would look like this:

.. code:: bash

  https://api.eth.events/es/block/search

ElasticSearch Clients
^^^^^^^^^^^^^^^^^^^^^
In order to use a default ElasticSearch client, you can provide the following parameters:

- **server**: *https://api.eth.events/es/*
- **index**: *ethereum-ethereum-mainnet-block*
- **type**: *block*
- **username**: *your email address*
- **password**: *your API key*

ElasticSearch Data Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following chapters will document the available entities and explain it's property structure.

.. toctree::
   :maxdepth: 2

   block
   tx
   log
   event
   call
