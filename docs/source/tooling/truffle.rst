.. _tooling.truffle:

Truffle
=======

**MythX for Truffle** is a `Truffle plugin <https://truffleframework.com/docs/truffle/getting-started/writing-external-scripts#third-party-plugin-commands>`_ that adds automated smart contract security analysis to the `Truffle framework <https://truffleframework.com>`_. With this plugin, you can run security analysis directly from your Truffle development environment.

The MythX plugin requires Truffle 5.0 or higher. Note that your Truffle project must compile
successfully for the security analysis to work.

Installation
------------

You can install the plugin on a per-project basis or globally.

.. warning:: 

   **Windows users** have reported potential issues with installation. You may have to install the following dependencies:

   * `Git <https://git-scm.com/>`_
   * `Windows Build Tools npm package <https://www.npmjs.com/package/windows-build-tools>`_::

       npm install --global --production windows-build-tools

     (This will need to be installed with Adminstrator privileges.)

Individual project
^^^^^^^^^^^^^^^^^^

Install the plugin on an individual Truffle project by running the following inside the root of your Truffle project::

  npm install truffle-security

The plugin will install for that Truffle project only. In addition, the plugin will **edit the project's configuration file** (``truffle-config.js``) to add the necessary plugin configuration. You do not need to edit this file.

.. note:: If you have existing plugins activated for the project, they will not be affected.

Global installation
^^^^^^^^^^^^^^^^^^^

Install the plugin globally so that it is accessible to all projects::

  npm install -g truffle-security

If you install MythX for Truffle in this manner, **you will in addition need to edit each project's configuration file** (``truffle-config.js``) to add the necessary plugin:

.. code-block:: javascript

   module.exports = {

     // ... 
 
       plugins: [ "truffle-security" ],
 
     // ... 

   };

Usage
-----

Analyzing an entire project
^^^^^^^^^^^^^^^^^^^^^^^^^^^

To run MythX for Truffle, run the following command in the root of your configured Truffle project::

  truffle run verify

.. note:: The project must compile successfully in order for the plugin to run. If the project hasn't been compiled yet, MythX for Truffle will try to compile it first.

Analyzing whole contract files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, all contracts in all contract files in the project will be analyzed. To analyze only a single contract file, use the following syntax::

  truffle run verify contract.sol

This will analyze all the contracts found in the file ``contract.sol``.

Multiple contract files can be specified here as well::

  truffle run verify contract1.sol contract2.sol

All contracts inside both ``contract1.sol`` and ``contract2.sol`` will be analyzed.

Analyzing specific contracts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can also analyze a specific contract::

  truffle run verify contract.sol:MyContract

This will analyze the contract named ``MyContract`` found in the file ``contract.sol``.

Multiple contracts can be specified here too. For example::

  truffle run verify contract1.sol:MyContract1 contract2.sol:MyContract2

This will analyze both ``MyContract1`` and ``MyContract2``, which are found in the ``contract1.sol`` and ``contract2.sol`` files respectively.

.. warning::

   The following syntax has been deprecated and should not be used::

     truffle run verify MyContract

Command options
---------------

To see the various command options available to you, run the following::

  truffle run verify --help


``--debug``
^^^^^^^^^^^

Provides additional debug output. Use ``--debug=2`` for more verbose output.

``--uuid <UUID>``
^^^^^^^^^^^^^^^^^

*(Experimental)* Prints in YAML results from a prior run having ``<UUID>``.

``--mode``
^^^^^^^^^^

Performs ``quick`` or in-depth (``full``) analysis.

``--style``
^^^^^^^^^^^

Outputs the report in the given `es-lint <https://eslint.org/docs/user-guide/formatters/>`_ style.

``--timeout <S>``
^^^^^^^^^^^^^^^^^

Limits MythX analyzes time to ``<S>`` seconds. The default is 120 seconds.

``--limit <N>``
^^^^^^^^^^^^^^^

Limit the pending analysis requests to no more than ``<N>`` at a time. As results come back, remaining contracts are submitted. The default is 10 contracts, the maximum value, but you can set this lower.

``--version``
^^^^^^^^^^^^^

Show package and MythX version information.

``--no-progress``
^^^^^^^^^^^^^^^^^

Will not display progress bars during analysis.


Accounts and access
-------------------

*You do not need to sign up for a MythX account in order to use the MythX plugin for Truffle.*

By default the plugin runs in Trial mode. **Trial mode returns a limited report**, with not all vulnerabilities listed. To get access to an unrestricted report, sign up for an account at https://mythx.io.

.. note:: Both free and paid plans are available. See :ref:`getting-started` for more details.

Once you have signed up for an account, you will need to add your account and password as environment variables on your system.

.. list-table::
   :header-rows: 1

   * - Environment variable
     - Value
   * - ``MYTHX_ETH_ADDRESS``
     - Your MythX account (Ethereum address)
   * - ``MYTHX_PASSWORD``
     - Your MythX password

You can temporarily add these environment variables to your terminal with the following commands (which will need to be customized with your account information):

* **Linux / macOS**:

  .. code-block:: console

     export MYTHX_ETH_ADDRESS=0x1234567891235678900000000000000000000000
     export MYTHX_PASSWORD='Put your password in here!'

* **Windows**:

  .. code-block:: console

     set MYTHX_ETH_ADDRESS=0x1234567891235678900000000000000000000000
     set MYTHX_PASSWORD='Put your password in here!'

Once you have done this, the MythX plugin should recognize your credentials and elevate your privileges.

.. seealso::

  * `MythX for Truffle (npm) <https://www.npmjs.com/package/truffle-security>`_
  * `MythX for Truffle (GitHub) <https://github.com/consensys/truffle-security>`_  