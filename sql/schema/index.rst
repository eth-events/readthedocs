Entity Relation Model
=====================

Overview
^^^^^^^^
Please also refer to the leading schema defined in :doc:`ElasticSearch <../../elastic/data-structure/index>`

SQL tables and data sources
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Blocks (*block*), Transactions (*tx*) and Logs (*log*) are coming directly from the Ethereum blockchain.
Traces (*trace*) are client specific - here we currently only save the data from our Parity nodes.
The Calls (*call*) and Events (*event*) tables contain some of our enriched data, e.g. the decoded name of the contract method (in method and event columns respectively) etc.

To enrich the data, we use the Contract (*contract*) and Token (*token*) tables to match the contract addresses and extract relevant information from the ABI.
As you can see, we are only able to make the data human-readable if we have the contract ABI.

If you are interested in monitoring your own (non-public) contract - `contact us <mailto:contact@eth.events>`_ and we can integrate your ABI so that you can interpret the data for your business case more easily.

The arguments of either the *Contract*, the *Call* or the *Event* are encoded as a JSON array in their enclosing tables.
In case of referencing a contract that would mean the constructor arguments at the time of creation.

ID fields (primary keys)
^^^^^^^^^^^^^^^^^^^^^^^^
The ID of the table *Trace* is the Keccak256 of:
``block-hash + _ + tx-hash + _ + transaction_index``

The ID of the table *Log* is the Keccak256 of:
``block-hash + _ + tx-hash + _ + log_index``

The ID of *Event* is inherited from the *Log* table, the *Call* ID is based on the *TX*.

All other ID fields should be self-explanatory. Ultimately you will rarely query data by the ID but instead using hashes, numbers and addresses.

Probability fields
^^^^^^^^^^^^^^^^^^
The *Contract* and *Token* tables contain fields for numeric probability.
Currently these are set to 1 for all data that we can retrieve from the blockchain or verify via `Etherscan <https://etherscan.io/>`_.
In case we're able to find a matching contract in our database by comparing the byte code of a contract or find a similar contract on a different blockchain, this is reflected in the probability.
The probabilities are then copied into the *Event* and *Call* tables to give an indication of how sure we are this is the right translation.

.. _sub-entities-jsonb:

Sub-Entities and their JSON representation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The sub entities - like arguments, links and traces - are encoded in their enclosing tables using the official JSON SQL-Type. Here are some resources to get familiar
with that data type:

- `JSON Datatype <https://www.postgresql.org/docs/current/datatype-json.html>`__
- `JSON Functions <https://www.postgresql.org/docs/current/functions-json.html>`__

All subentities are stored using the PostgreSQL-Type **JSONB**.

Full Data model for the Ethereum SQL index
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. figure:: eth-events-er-model.svg
  :alt: Full Data model for the Ethereum SQL index

  Full Data model for the Ethereum SQL index
