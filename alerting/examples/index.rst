Alerting Examples
=================

Kovan DAI Transfer
^^^^^^^^^^^^^^^^^^

.. literalinclude:: ./kovanDaiTransfer.json
   :language: json

Kovan ETH Traces
^^^^^^^^^^^^^^^^^^

.. literalinclude:: ./kovanEthTraces.json
   :language: json

Full Alerting
^^^^^^^^^^^^^
Usage of all possible alert-triggers were all events (decoded logs) are matched that have:

- ``address`` = 0xe3818504c1B32bF1557b16C238B2E01Fd3149C17
- ``event`` = Transfer
- ``to`` = 0x8d12A197cB00D4747a1fe03395095ce2A5CC6819
- ``value`` > 999999

.. literalinclude:: ./full.json
   :language: json
