ElasticSearch Clients
=====================
In order to use a default ElasticSearch client, you can provide the following parameters:

- **server**: *https://api.anyblock.tools/ethereum/ethereum/mainnet/es/*
- **index**: *ethereum-ethereum-mainnet-block*
- **type**: *block*
- **username**: *your email address*
- **password**: *your API key*

The following example shows how to fetch the latest 5 DAI transfers from ElasticSearch in Node.js

.. code-block:: js

  const Client = require('elasticsearch').Client

  const esClient = new Client({
    hosts: 'https://api.anyblock.tools/ethereum/ethereum/mainnet/es/',
    httpAuth: 'your-email-address:your-api-key',
  })

  esClient.search({
    index: 'ethereum-ethereum-mainnet-event',
    type: 'event',
    body: {
      query: {
        bool: {
          filter: [
            {
              term: {
                'address.raw': '0x89d24A6b4CcB1B6fAA2625fE562bDD9a23260359'
              }
            },
            {
              term: {
                'event.raw': 'Transfer'
              }
            }
          ]
        }
      },
      sort: {
        timestamp: 'desc'
      },
      size: 5
    }
  })
  .then(result => console.log(require('util').inspect(result, { depth: null })))
  .catch(err => console.error(err))
