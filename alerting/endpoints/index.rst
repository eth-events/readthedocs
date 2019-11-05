Alerting API-Routes
"""""""""""""""""""
When adding or modifying alerting rules via the API, you have to provide the metadata you can just select in the frontend. The actual configuration goes into the config section.

.. code:: json

    {
        "name": "Example Alerting Rule 0001",
        "maxConfirmationCount": 10,
        "technology": "ethereum",
        "blockchain": "ethereum",
        "network": "kovan",
        "config": {
            "see": "examples"
        }
    }


The available routes are:

Get all Alerting Rules
----------------------
.. code:: bash

    curl -X GET \
    https://api.eth.events/alerting/rules/ \
    -H 'Authorization: Bearer <your-token>'


Get a single Alerting Rule
--------------------------
.. code:: bash

    curl -X GET \
    https://api.eth.events/alerting/rules/<id>/ \
    -H 'Authorization: Bearer <your-token>'


Add an Alerting Rule
--------------------
.. code:: bash

    curl -X POST \
    https://api.eth.events/alerting/rules/ \
    -H 'Authorization: Bearer <your-token>' \
    -H 'Content-Type: application/json' \
    -d '{
            "name": "Example Alerting Rule 0001",
            "maxConfirmationCount": 10,
            "technology": "ethereum",
            "blockchain": "ethereum",
            "network": "kovan",
            "config": {
                "see": "examples"
            }
        }'


Update an Alerting Rule
-----------------------
.. code:: bash

    curl -X PUT \
    https://api.eth.events/alerting/rules/<id>/ \
    -H 'Authorization: Bearer <your-token>' \
    -H 'Content-Type: application/json' \
    -d '{
            "name": "Example Alerting Rule 0002",
            "maxConfirmationCount": 5,
            "config": {
                "see": "examples"
            }
        }'

Delete an Alerting Rule
-----------------------
.. code:: bash

    curl -X DELETE \
    https://api.eth.events/alerting/rules/<id>/ \
    -H 'Authorization: Bearer <your-token>'
