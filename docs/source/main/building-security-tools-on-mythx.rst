MythX API Developer Guide
=========================

This section of the guide is aimed at developers who want build security tools using the MythX API.

.. contents:: :local:


API Specification
-----------------

Besides whatever you might find in this guide, the `MythX OpenAPI Spec <https://api.mythx.io/v1/openapi>`_
is the ultimate authority. Beyond that be dragons.


Language Bindings
-----------------

In most cases you'll want to use an existing client library that abstracts the low-level details of
interacting with MythX.

.. toctree::
    :maxdepth: 1

    ../SDK/armlet
    ../SDK/sabre
    ../SDK/shard


Experimenting with MythX API
----------------------------

The `MythX API curl scripts <https://github.com/rocky/mythx-api-curl>`_ demonstrate
how clients interact with the API at the most basic level. The scripts will show
you the HTTP requests that get sent as well with the JSON output returned as the result
of each request.

The process for analyzing a smart contract works as follows:

* Submit a contract for analysis, creating a job run with a UUID
* See the status of job using the UUID of a previously submitted analysis
* Get the results of a previously finished analysis using the UUID

After ensuring you have the prerequisites programs, set
`MYTHX_PASSWORD` to and one of `EMAIL` or `MYTHX_ETH_ADDRESS` to
values that have been registered. For example:

.. code-block:: console

  $ export MYTHX_PASSWORD=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

  $ # Only one of two below is needed:
  $ export EMAIL=me@example.com
  $ export MYTHX_ETH_ADDRESS=0x.............

Above `MYTHX_API_URL` is optional and the default value is given above.
We have however a number of API servers. If you are using one or using
your own private version, set the URL host accordingly.

From the above, you now need to get a `MYTHX_ACCESS_TOKEN` environment
variable set up. To do that run:

.. code-block:: console

   $ . ./login.sh
   Successfully logged into MythX



.. code-block:: console

  $ ./api-version.sh
  Issuing HTTP GET https://api.mythx.io/v1/version
  curl completed successfully. Output follows...
  HTTP/1.1 200 OK
  v1.0.20



Submitting an Analysis Job
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

  $ ./analyses.sh sample-json/PublicArray.js
  Issuing HTTP POST http://api.mythx.io/v1/analyses
    (with MYTHX_API_KEY and EVM bytecode)
  curl completed successfully. Output follows...
  HTTP/1.1 200 OK
  {
    "result": "Queued",
    "uuid": "bf9fe267-d322-4641-aae2-a89e62f40770"
  }


Polling the API to Request Job Status
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

  $ ./analyses-status.sh "bf9fe267-d322-4641-aae2-a89e62f40770"
  Issuing HTTP GET http://api.mythx.io/v1/analyses/bf9fe267-d322-4641-aae2-a89e62f40770
    (with MYTHX_API_KEY)
  curl completed successfully. Output follows...
  HTTP/1.1 200 OK
  {
    "result": "Finished",
    "uuid": "bf9fe267-d322-4641-aae2-a89e62f40770"
  }


Obtaining Analysis Results
^^^^^^^^^^^^^^^^^^^^^^^^^^

TODO


Writing a Simple MythX Client in JavaScript
-------------------------------------------





