Basic SQL Usage Examples
========================

Welcome!
--------

Within this tutorial you will learn how to retrieve and analyze data
from the Ethereum Blockchain with the help of the eth.events SQL interface.

We will show you how to retrieve data from eth.events using common SQL language.

What you must know already
--------------------------

This tutorial is written for programmers, who have some experience with SQL. You should also have visited the :doc:`authorization <../authorization/index>`
page and setup our connection to the database.
Remember that the subentities are stored using the Postgresql-Type **JSONB**.
For more information on that, please take a look at the :ref:`ER model <sub-entities-jsonb>`.

Basic eth.events SQL queries
----------------------------

Choose one of the databases available. All of them are encoded as the triple of:

.. code:: bash

  <technology>_<chain>_<network>

The main chain is named `ethereum_ethereum_mainnet`.

After choosing a blockchain, you might continue with the example queries.

Find the latest block
~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM block ORDER BY number DESC LIMIT 1

This will show the whole block. But you can use a shorter form:

.. code:: SQL

  SELECT max(number) FROM block

Find events for a given block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM event
  WHERE event.block_number = 7075271

Find calls for a transaction hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM call
  WHERE call.hash = '0xadd837afa5b68987eb9f0167ad65cbb8131f57da84db56a19acf4a5a98bd35da'

Find transactions for a given contract
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For our example we use the address of the TenXPay token contract:

.. code:: SQL

  SELECT * FROM tx
  WHERE tx.to = '0xB97048628DB6B661D4C2aA833e95Dbe1A905B280'
  LIMIT 100

Find specific events for a given contract
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For our example we use the address of the TenXPay token contract again, however we
would like to know the values of transfers greater than *1ETH*:

.. code:: SQL

  SELECT arg->'scaled', arg ->'num'
  FROM "event",jsonb_array_elements(args) arg
  WHERE event = 'Transfer' AND address = '0xB97048628DB6B661D4C2aA833e95Dbe1A905B280'
  AND (arg->'num')::numeric > 1000000000000000000
  LIMIT 100

Find the latest 10 DAI Transfer events and extract sender, receiver and value from JSON
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT 
  	*,
  	args->0->>'hex' as "from",
  	args->1->>'hex' as "to",
  	CAST(args->2->'scaled' AS NUMERIC) AS "value"
  FROM event
  WHERE address = '0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359'
  AND event = 'Transfer'
  ORDER BY timestamp DESC
  LIMIT 10

Where to go from here
~~~~~~~~~~~~~~~~~~~~~

You may continue with taking a look at the :doc:`Elasticsearch tutorial <../../elastic/tutorials/index>`.
Please let us know if you have any further questions or need some help with your application.
