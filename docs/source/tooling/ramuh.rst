Ramuh, MythX Desktop Notifications
==================================

Ramuh brings the power of the MythX Platform API to your desktop.

It watches directories for changes on smart contract files, sends
data to MythX security analysis platform and shows relevant security
issues found on your code as desktop notifications.

How to use
----------

First, install ramuh package:
.. code-block:: console

    $ npm i -g ramuh

For using ramuh you need MythX platform credential, either as an API key
or as a eth address and password pair. Ramuh expects these values to be set
as the environment variables `MYTHX_API_KEY` or `MYTHX_ETH_ADDRESS` and
`MYTHX_PASSWORD`.
Then, start it indicating MythX platform access credentials and the
directory to watch:
.. code-block:: console

    $ ramuh -contractspath /path/to/contracts

From this point, when you change `*.sol` files in `/path/to/contracts`, an
analysis request is sent to the MythX API endpoint. If any security issue is
detected, it will be shown to you as a desktop notification.

This video shows how all this works:

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/MQxYBHuYeEA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


.. seealso::

  * `The github project <https://github.com/ConsenSys/ramuh>`_
