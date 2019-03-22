MythX Security Analysis plugin for Truffle
==========================================

MythX Security Analysis plugin for Truffle adds automated smart contract security analysis to the `Truffle framework <https://truffleframework.com>`_.

Prerequisites
^^^^^^^^^^^^^

The MythX plugin is compatible with Truffle 5.0 or higher. Note that your Truffle project must compile
successfully for the security analysis to work.

Quickstart
^^^^^^^^^^

Install the plugin by running:

.. code-block:: console

  $ npm install truffle-security

Currently, the plugin must be activated on a per-project basis. Add the following to `truffle.js` in your Truffle project directory:

.. code-block:: console

  module.exports = {
      plugins: [ "truffle-security" ]
  };

By default, the plugin is configured with a MythX trial account that
allows for limited access. Sign up for a free account to get
full access (see :ref:`getting-started`).

.. code-block:: console

  export MYTHX_ETH_ADDRESS=0x1234567891235678900000000000000000000000
  export MYTHX_PASSWORD='Put your password in here!'


Installing the plugin adds the `truffle run verify` command. You can
launch a security analysis of your project by running:

.. code-block:: console

    $ truffle run verify

Note that the project must compile successfully in order for security
analysis to work.

Add the `--help` flag to display additional options:

.. code-block:: console

    $ truffle run verify --help

.. seealso::

  * `npm package <https://www.npmjs.com/package/truffle-security>`_
  * `GitHub repository <https://github.com/consensys/truffle-security>`_
  