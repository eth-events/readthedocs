.. eth.events documentation master file, created by
   sphinx-quickstart on Wed May 30 15:50:23 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to eth.events's documentation!
======================================

eth.events is a hosted Ethereum API providing sophisticated support to search, filter and aggregate events from the Ethereum blockchain, and it is based on Elasticsearch.

Constructing a query and understanding what an eth.events server returns is the most important skill you need in order to get started with eth.events.

If you are new to **Elasticsearch** and eth.events, you first should:

- Inform yourself about the :doc:`elastic-authorization <elastic/authorization/index>` methods
- Read our :doc:`elastic developer tutorial <elastic/tutorials/query>`
- Familiarise yourself with the `Elasticsearch Query DSL <https://www.elastic.co/guide/en/elasticsearch/reference/6.5/query-dsl.html>`__.
- Understand the elastic-schema and how events are :doc:`mapped <elastic/endpoints/index>`
- Leverage our :doc:`example queries <elastic/example-queries/index>` and build your own queries.

You might also take a look at our **SQL** interface:

- Check for the :doc:`sql-access <sql/authorization/index>` to our database
- Maybe start with looking at the :doc:`entity-relation model <sql/schema/index>`
- To get a quickstart on how to use the interface you should see the :doc:`sql tutorial <sql/tutorials/sql>`

Please also visit our main `Website <https://eth.events>`__ or in case you have any further questions.

.. toctree::
   :caption: Documentation Contents:
   :glob:
   :maxdepth: 2

   elastic/*
   sql/*

.. Indices and tables
.. ==================
..
.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`
