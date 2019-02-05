Entity Relation Model
=====================

Overview
^^^^^^^^
Please also refer to the leading schema defined in elastic :doc:`elastic </elastic/endpoints/index>`

SQL tables and data sources
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Blocks (*Block*), transactions (*TX*) and logs (*Log*) are coming from the Ethereum blockchain. 
*Trace* and *InternalTrace* are client specific - here we only save the data from our Parity node.
The *Call* and *Event* table contain some of our enriched data, e.g. the decoded name of the contract method (in method and event columns respectively). 
To enrich the data, we use the tables *Contract* and *Token* to match the hashes etc. 
As you can see, we are only able to make the data human-readable if we have the contract ABI. 
If you are interested in monitoring your own (non-standard) contract - `contact us <mailto:contact@eth.events>`_ and we can integrate your ABI 
so that you can interpret the data for your business case more easily.
Most data in *Contract* and *Token* is pulled from Etherscan at the moment. 
Particularly regarding contract ABIs we have been in talks about establishing an independent registry.
If you want to help or can provide funding to support this mission to help the whole Ethereum ecosystem - please `contact us <mailto:contact@eth.events>`_.
The arguments of either the *Contract*, the *Call* or the *Event* are encoded as a JSON array in their enclosing tables.
In case of referencing a contract that would mean the constructor arguments at the time of creation.

ID fields (primary keys)
^^^^^^^^^^^^^^^^^^^^^^^^
The ID (primary key) of the table *Trace* is composed of Keccak256 of:
``block-hash + _ + tx-hash + _ + transaction_index``

The ID (primary key) of the table *Log* is composed of Keccak256 of: 
``block-hash + _ + tx-hash + _ + log_index``

The ID of *Event* is inherited from *Log* table.
All other ID fields should be self-explanatory.

Probability fields
^^^^^^^^^^^^^^^^^^
The *Contract* and *Token* tables contain fields for numeric probability. 
Currently it is set to 1 for all data that we can retrieve from the blockchain or verify via Etherscan. 
In the near future we plan to compare new contracts on the blockchain against existing ones in order to identify the type 
(e.g. ERC-20 token, Augur prediction markets, etc.) and enable automatic decoding of events as much as possible.
These probabilities are also reflected in the *Call* and *Event* table.

.. _sub-entities-jsonb:

Sub-Entities and their JSON representation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The sub entities - like arguments, links and traces - are encoded in their enclosing tables using the official JSON SQL-Type. Here are some resources to get familiar
with that data type:

- `JSON Datatype <https://www.postgresql.org/docs/current/datatype-json.html>`__
- `JSON Functions <https://www.postgresql.org/docs/current/functions-json.html>`__

All subentities are stored using the Postgresql-Type **JSONB**.

Full Data model for the Ethereum SQL index
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. figure:: er-model.png
  :alt: Full Data model for the Ethereum SQL index

  Full Data model for the Ethereum SQL index