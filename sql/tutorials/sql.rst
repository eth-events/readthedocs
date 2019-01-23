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

Find events and their arguments for a given block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM event 
    JOIN arg 
      ON event.id = arg.event_id 
  WHERE event.block_number = 7075271

Find calls and their arguments for a transaction hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM call
    JOIN arg 
      ON call.id = arg.call_id 
  WHERE call.hash = '0xadd837afa5b68987eb9f0167ad65cbb8131f57da84db56a19acf4a5a98bd35da'

Find traces for a transaction hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM trace
    JOIN internaltrace AS traces
      ON trace.id = traces.trace_id 
  WHERE trace.transaction_hash = '0x9994f38854f80b430b4708d356bf201154055d846c63bedab25deee329066cd4'

Find transactions for a given contract
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For our example we use the address of the TenXPay token contract:

.. code:: SQL

  SELECT * FROM tx
  WHERE tx."to" = LOWER('0xB97048628DB6B661D4C2aA833e95Dbe1A905B280') 
  LIMIT 100

Where to go from here
~~~~~~~~~~~~~~~~~~~~~

You may continue with taking a look at the :doc:`Elasticsearch tutorial <../../elastic/tutorials/index>`.
Please let us know if you have any further questions or need some help with your application.
