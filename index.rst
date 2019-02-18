.. eth.events documentation master file, created by
   sphinx-quickstart on Wed May 30 15:50:23 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to eth.events's documentation!
======================================

eth.events is a hosted Ethereum API providing sophisticated support to search, filter and aggregate events from multiple Ethereum based blockchains. It is based on Elasticsearch and PostgreSQL.

Constructing a query and understanding what the eth.events server returns is the most important skill you need in order to get started with eth.events.

If you are new to **ElasticSearch** and / or the **eth.events API**, you first should:

- Inform yourself about the :doc:`authorization <api/authorization/index>` methods
- Read our :doc:`elastic developer tutorial <elastic/tutorials/query>`
- Familiarise yourself with the `Elasticsearch Query DSL <https://www.elastic.co/guide/en/elasticsearch/reference/6.5/query-dsl.html>`__.
- Understand the elastic-schema and how events are :doc:`mapped <elastic/data-structure/index>`
- Leverage our :doc:`example queries <elastic/example-queries/index>` and build your own queries.

You might also want to take a look at our **SQL** interface:

- Check the :doc:`sql-access <sql/authorization/index>` to our database
- Maybe start with looking at the :doc:`entity-relation model <sql/schema/index>`
- To get a quickstart on how to use the interface you should see the :doc:`sql tutorial <sql/tutorials/sql>`

Please also visit our main `Website <https://eth.events>`__ and get in touch. We're always interested in what you're BUIDLing.

.. toctree::
   :caption: Documentation Contents:
   :glob:
   :maxdepth: 2

   api/*
   elastic/*
   sql/*

.. Indices and tables
.. ==================
..
.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`
