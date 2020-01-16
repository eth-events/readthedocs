Example queries
===============

The following queries are meant to be a building block for
your own anyblock.tools queries.

You also will need a registered anyblock.tools API-Account in order to run the
REST calls. Keep in mind to replace the ``$mytoken`` variable in the ``cURL`` commands with your personal API token.

.. contents::
        :local:


Block
~~~~~

Get block by blockhash
----------------------
The results will contain only the block with the given block `number`.
This requires no body.

.. code:: bash

    GET /ethereum/ethereum/mainnet/es/block/0xf44f60a66257d1c6c8afd2a64aaeb306d9c471d5d38b6dc277811455192ecee1/


Select by block number
----------------------

The results will contain only number selected with the given term.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/block/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": {
          "term": {
            "number.num": 6600000
          }
        }
      }
    },
    "_source": ["number.num"]
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
  https://api.anyblock.tools/ethereum/ethereum/mainnet/es/block/search/ \
  -H 'Authorization: Bearer $mytoken' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": {
      "bool": {
        "filter": {
          "term": {
            "number.num": 6600000
          }
        }
      }
    },
    "_source": ["number.num"]
  }'



Filter last 5 known blocks (sorted)
-----------------------------------

The results will only contain the 5 most recent blocks (highest block number) on the index.
Sorted in descending order (highest block number first).

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/block/search/

JSON body:

.. code-block:: json

  {
    "sort": {
      "number.num": "desc"
    },
    "size": 5
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
  https://api.anyblock.tools/ethereum/ethereum/mainnet/es/block/search/ \
  -H 'Authorization: Bearer $mytoken' \
  -H 'Content-Type: application/json' \
  -d '{
    "sort": {
      "number.num": "desc"
    },
    "size": 5
  }'


Transaction
~~~~~~~~~~~

Filter by the transaction's block's hash
----------------------------------------

The results will contain all transactions that are included in the
specified block, identified with it's `blockHash`.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/tx/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "blockHash": "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
            }
          }
        ]
      }
    },
    "size": 200
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
  https://api.anyblock.tools/ethereum/ethereum/mainnet/es/tx/search/ \
  -H 'Authorization: Bearer $mytoken' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "blockHash": "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
            }
          }
        ]
      }
    },
    "size": 200
  }'

Filter by a range of block numbers
----------------------------------

The results will contain all transactions, that are included in
a block, that is within the specified boundaries of the block number
range. The block number has to be greater than or equal to 6400000 (`gte`)
and less than or equal to 6500000 (`lte`).
The results will show a maximum of 200 blocks, in no particular order.


HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/tx/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "range": {
              "blockNumber.num": {
                "gte": 6400000,
                "lte": 6500000
              }
            }
          }
        ]
      }
    },
    "size": 200
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
  https://api.anyblock.tools/ethereum/ethereum/mainnet/es/tx/search/ \
  -H 'Authorization: Bearer $mytoken' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": {
      "bool": {
        "filter": [
          {
            "range": {
              "blockNumber.num": {
                "gte": 6400000,
                "lte": 6500000
              }
            }
          }
        ]
      }
    },
    "size": 200
  }'


Filter by receiving or originating address
------------------------------------------

The results will contain all transactions, whose sender (`from`) or receiver (`to`) is
has the specified address.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/tx/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "should": [
          {
            "term": {
              "from": "0xa1e4380a3b1f749673e270229993ee55f35663b4"
            }
          },
          {
            "term": {
              "to": "0xa1e4380a3b1f749673e270229993ee55f35663b4"
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/tx/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '{
      "query": {
        "bool": {
          "should": [
            {
              "term": {
                "from": "0xa1e4380a3b1f749673e270229993ee55f35663b4"
              }
            },
            {
              "term": {
                "to": "0xa1e4380a3b1f749673e270229993ee55f35663b4"
              }
            }
          ]
        }
      }
    }'



Select by transaction hash
--------------------------

The results will contain only the transaction with the given transaction `hash`.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/tx/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "_id": "0x5c504ed432cb51138bcf09aa5e8a410dd4a1e204ef84bfed1be16dfba1b22060"
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/tx/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '  {
      "query": {
        "bool": {
          "filter": [
            {
              "term": {
                "_id": "0x5c504ed432cb51138bcf09aa5e8a410dd4a1e204ef84bfed1be16dfba1b22060"
              }
            }
          ]
        }
      }
    }'


Log
~~~

Filter by causing transaction's sender
--------------------------------------

The results will contain all logs, where the sender of the transaction that caused the log to be emitted
has the specified address.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/log/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "transactionHash": "0xca9b47a8bfd1c8c0e184992e0a2714558603182fc4a7f2ac16cf16f6be4f0a2a"
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/log/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '{
        "query": {
          "bool": {
            "filter": [
              {
                "term": {
                  "transactionHash": "0xca9b47a8bfd1c8c0e184992e0a2714558603182fc4a7f2ac16cf16f6be4f0a2a"
                }
              }
            ]
          }
        }
      }'



Filter by emitting contract
---------------------------

The results will contain all logs that were emitted from the specified contract.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/log/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "address": "0x12459c951127e0c374ff9105dda097662a027093"
            }
          }
        ]
      }
    },
    "size": 100
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/log/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '{
      "query": {
        "bool": {
          "filter": [
            {
              "term": {
                "address": "0x12459c951127e0c374ff9105dda097662a027093"
              }
            }
          ]
        }
      },
      "size": 100
    }'


Event
~~~~~

Filter by event name
--------------------
The results will contain all events with the specified event name.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/event/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "event": "transfer"
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/event/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '{
      "query": {
        "bool": {
          "filter": [
            {
              "term": {
                "event": "transfer"
              }
            }
          ]
        }
      }
    }'


Filter by emitting contract
---------------------------

The results will contain all events that where emitted by the specified contract.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/event/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "address.raw": "0xcfb98637bcae43C13323EAa1731cED2B716962fD"
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/event/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '{
      "query": {
        "bool": {
          "filter": [
            {
              "term": {
                "address.raw": "0xcfb98637bcae43C13323EAa1731cED2B716962fD"
              }
            }
          ]
        }
      }
    }'


Filter by ERC20 contract's address and `from` address
-----------------------------------------------------

The results will contain all events that where emitted by the specified contract, and where the
`from` argument of the event matches the specifid address. Although this query is tailored for ERC20 contracts,
there is no parameter that specifically filters for the ERC20 interface.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/event/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "filter": [
          {
            "term": {
              "address.raw": "0xcfb98637bcae43C13323EAa1731cED2B716962fD"
            }
          },
          {
            "nested": {
              "path": "args",
              "query": {
                "bool": {
                  "filter": [
                    {
                      "term": {
                        "args.name": "_from"
                      }
                    },
                    {
                      "term": {
                        "args.value.hex": "0x59a5208B32e627891C389EbafC644145224006E8"
                      }
                    }
                  ]
                }
              }
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/event/search/ \
    -H 'Authorization: Bearer $mytoken' \
    -H 'Content-Type: application/json' \
    -d '{
      "query": {
        "bool": {
          "filter": [
            {
              "term": {
                "address.raw": "0xcfb98637bcae43C13323EAa1731cED2B716962fD"
              }
            },
            {
              "nested": {
                "path": "args",
                "query": {
                  "bool": {
                    "filter": [
                      {
                        "term": {
                          "args.name": "_from"
                        }
                      },
                      {
                        "term": {
                          "args.value.hex": "0x59a5208B32e627891C389EbafC644145224006E8"
                        }
                      }
                    ]
                  }
                }
              }
            }
          ]
        }
      }
    }'


Specialised queries
~~~~~~~~~~~~~~~~~~~

Find entity by hash
-------------------

The results will contain either a block with the specified block hash or all transactions, whose sender (`from`) or receiver (`to`) has the specified address.
Queries like this are useful if the type of the entity that a hash represents is not known in advance.

HTTP-Method/Endpoint:

.. code:: bash

      POST /ethereum/ethereum/mainnet/es/block,tx/search/

JSON body:

.. code-block:: json

  {
    "query": {
      "bool": {
        "should": [
          {
            "ids": {
              "values": [
                "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
              ]
            }
          },
          {
            "term": {
              "from": "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
            }
          },
          {
            "term": {
              "to": "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
            }
          }
        ]
      }
    }
  }

Execute the request with ``cURL``:

.. code:: bash

  curl -X POST \
    https://api.anyblock.tools/ethereum/ethereum/mainnet/es/block,tx/search/ \
    -H 'Authorization: Bearer d2560f14-1935-44e7-ad3e-a1718dc03bd2' \
    -H 'Content-Type: application/json' \
    -d '{
      "query": {
        "bool": {
          "should": [
            {
              "ids": {
                "values": [
                  "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
                ]
              }
            },
            {
              "term": {
                "from": "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
              }
            },
            {
              "term": {
                "to": "0x4e3a3754410177e6937ef1f84bba68ea139e8d1a2258c5f85db9f1cd715a1bdd"
              }
            }
          ]
        }
      }
    }'
