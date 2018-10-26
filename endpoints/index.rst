Index endpoints
======================================

Eth.events currently generates endpoint paths for the composition of the following triple:

- `technology`
- `blockchain`
- `network`

Most users will be interested in the triple `/ethereum/ethereum/mainnet/`.

Following the triple you may choose between the current available operations:

- `search`
- `_search`
- `count`
- `_count`

After choosing an operation you have access to the following entities on the Ethereum blockchain:

- `block` 
- `tx`
- `log`
- `event`
- `call`
- `contract`
- `token`

Searches on the eth.events index can address a specific endpoint, so that the endpoint itself
already functions as a filter for the specified entity.


- For example, a search request to `/ethereum/ethereum/mainnet/search/event/` will only show `event` typed objects.

.. TODO provide copy+pasteable command


Endpoints also can be combined, to widen the scope of the query:

- A search request to `/ethereum/ethereum/mainnet/search/event,tx/` will only show `event` and `tx` typed objects.

.. TODO provide copy+pasteable command

The following chapters will document the available entities and explain it's property structure.

.. toctree::
   :maxdepth: 2

   block
   tx
   log
   event
   call
   contract
   token
