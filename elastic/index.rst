ElasticSearch
=============

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

It's also possible to explicitly provide the desired index in the URL which follows the format **$technology**-**$blockchain**-**$network**-**$resource**. This is completely optional but required for ElasticSearch client compatibility and is normally derrived from the selected network and resource, but must match the network and resource if present.

A simple query for the latest block would look like this:

.. code:: bash

  https://api.eth.events/es/block/search


.. toctree::
   :maxdepth: 2

   clients/index
   data-structure/index
   data-types/index
   example-queries/index
   tutorials/index
