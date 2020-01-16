Index endpoints
===============

When interacting with the anyblock.tools API, the base URL structure is always as follows:

/*$technology*/*$blockchain*/*$network*/*$interface*/...

The first triple of *technology*, *blockchain* and *network* describes the network you want to interact with. For most users this would be **/ethereum/ethereum/mainnet/**, which is also the default and can be omitted. Other possible values would be for example */ethereum/classic/morden/*.

The fourth part is the search interface you want to use. Currently only the ElasticSearch interface **/es/** is supported, but we're already working on SQL and GraphQL support.

So, for most users the base URL will be

.. code:: bash

  https://api.anyblock.tools/ethereum/ethereum/mainnet/es/
