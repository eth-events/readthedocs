Welcome to anyblock.tools's documentation!
======================================

Anyblock.tools is a hosted Ethereum API providing sophisticated support to search, filter and aggregate events from multiple Ethereum based blockchains. It is based on Elasticsearch and PostgreSQL.

Constructing a query and understanding what the anyblock.tools server returns is the most important skill you need in order to get started with anyblock.tools.

If you are new to **ElasticSearch** and / or the **anyblock.tools API**, you first should:

- Inform yourself about the :doc:`authorization <api/authorization/index>` methods
- Read our :doc:`elastic developer tutorial <elastic/tutorials/query>`
- Familiarise yourself with the `Elasticsearch Query DSL <https://www.elastic.co/guide/en/elasticsearch/reference/6.5/query-dsl.html>`__.
- Understand the elastic-schema and how events are :doc:`mapped <elastic/data-structure/index>`
- Leverage our :doc:`example queries <elastic/example-queries/index>` and build your own queries.

You might also want to take a look at our **SQL** interface:

- Check the :doc:`sql-access <sql/authorization/index>` to our database
- Maybe start with looking at the :doc:`entity-relation model <sql/schema/index>`
- To get a quickstart on how to use the interface you should see the :doc:`sql tutorial <sql/tutorials/sql>`

You may also find here help for our **ALERTING** dashboard:

- Visit :doc:`alerting <alerting/general/index>` to understand how our alerting works
- `Contact us <mailto:contact@anyblockanalytics.com>`__ to get access to the alerting feature

Please also visit our main `Website <https://anyblock.tools>`__ and get in touch. We're always interested in what you're BUIDLing.

.. toctree::
   :caption: Documentation Contents:
   :glob:
   :maxdepth: 2

   api/*
   elastic/*
   sql/*
   alerting/*

.. Indices and tables
.. ==================
..
.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`
