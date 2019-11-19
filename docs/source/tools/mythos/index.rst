.. meta::
   :description: How to use and install Mythos, which helps you run security scans on a smart contract right in your console, returning the output with source code mapping.

.. _tools.mythos:

Mythos
======

Mythos helps you run scans right in your console, returning the output with source code mapping.

Install Mythos
--------------

You must have nodejs_ and npm_ installed on your system.

.. code-block:: console

    $ npm install @cleanunicorn/mythos


Usage
----------------------

First of all you need to have an active account created on the MythX_ platform. 

You need to specify your Ethereum address and the password that you generated on the platform.

I prefer to add them to the console as environment variables:

.. code-block:: console

    $ export MYTHX_ETH_ADDRESS='mythxEthAddress'
    $ export MYTHX_PASSWORD='mythxPassword'

And then you can start the scan:

.. code-block:: console

    $ mythos analyze ./contract.sol Contract

But you can also specify them as flags ``--mythxEthAddress=mythxEthAddress`` and ``--mythxPassword=mythxPassword`` when running the tool.

Check the GitHub_ page and star the project, open an issue if you need more functionality or have some kind of problem.

It is a work in progress so any feedback is appreciated and your input will help shape the tool to fit your needs.

.. _nodejs: https://nodejs.org/en/ 
.. _npm: https://www.npmjs.com/
.. _mythX: https://mythx.io
.. _GitHub: https://github.com/cleanunicorn/mythos