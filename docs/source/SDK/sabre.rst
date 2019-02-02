Minimum Viable JavaScript CLI
=============================

Sabre is a JavaScript-based CLI for the MythX platform. It has been
implemented as a PoC for API integration.

Usage
-----

.. code-block:: console

    $ export MYTHX_API_KEY=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    $ export MYTHX_API_URL=https://api.myhthril.ai/
    $ node sabre.js mycontract.sol

    __mycontract.sol __
    3     Low     State Variable Default Visibility    https://smartcontractsecurity.github.io/SWC-registry/docs/SWC-108
    5     Low     Function Default Visibility          https://smartcontractsecurity.github.io/SWC-registry/docs/SWC-100
    14    High    Reentrancy                           https://smartcontractsecurity.github.io/SWC-registry/docs/SWC-107


.. seealso::

  * `The GitHub project <https://github.com/b-mueller/sabre>`_
