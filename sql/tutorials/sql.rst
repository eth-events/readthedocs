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

Find the latest block
~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM ethereum_ethereum_mainnet_block ORDER BY number DESC LIMIT 1

This will show the whole block. But you can use a shorter form:

.. code:: SQL

  SELECT max(number) FROM ethereum_ethereum_mainnet_block 

Find events and their arguments for a given block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM ethereum_ethereum_mainnet_event 
    JOIN ethereum_ethereum_mainnet_arg 
      ON ethereum_ethereum_mainnet_event.id = ethereum_ethereum_mainnet_arg.event_id 
  WHERE ethereum_ethereum_mainnet_event.block_number = 7075271

Find calls and their arguments for a transaction hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM ethereum_ethereum_mainnet_call AS call
    JOIN ethereum_ethereum_mainnet_arg 
      ON call.id = ethereum_ethereum_mainnet_arg.call_id 
  WHERE call.hash = '0xadd837afa5b68987eb9f0167ad65cbb8131f57da84db56a19acf4a5a98bd35da'

Find traces for a transaction hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: SQL

  SELECT * FROM ethereum_ethereum_mainnet_trace AS trace
    JOIN ethereum_ethereum_mainnet_internaltrace AS traces
      ON trace.id = traces.trace_id 
  WHERE trace.transaction_hash = '0x9994f38854f80b430b4708d356bf201154055d846c63bedab25deee329066cd4'

Find transactions for a given contract
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For our example we use the address of the TenXPay token contract:

.. code:: SQL

  SELECT * FROM ethereum_ethereum_mainnet_tx AS TX 
  WHERE TX."to" = LOWER('0xB97048628DB6B661D4C2aA833e95Dbe1A905B280') 
  LIMIT 100

Where to go from here
~~~~~~~~~~~~~~~~~~~~~

You may continue with taking a look at the :doc:`Elasticsearch tutorial <../../elastic/tutorials/index>`.
Please let us know if you have any further questions or need some help with your application.
