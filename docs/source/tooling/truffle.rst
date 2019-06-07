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

   **Windows users** need to install the following dependencies:

   * `Git <https://git-scm.com/>`_
   * `Windows Build Tools npm package <https://www.npmjs.com/package/windows-build-tools>`_::

       npm install --global --production windows-build-tools

   Both will need to be installed with Administrator privileges.

   In addition, those using **Windows PowerShell** may need to set the `Execution Policy <https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy>`_ to Unrestricted in order to install the Windows Build Tools package::

     Set-ExecutionPolicy Unrestricted

   This will also need to be run with Administrator privileges.

Individual project
^^^^^^^^^^^^^^^^^^

Install the plugin on an individual Truffle project by running the following inside the root of your Truffle project::

  npm install truffle-security

The plugin will install for that Truffle project only. In addition, the plugin will **edit the project's configuration file** (``truffle-config.js``) to add the necessary plugin configuration. You do not need to edit this file.

.. note:: If you have existing plugins activated for the project, they will not be affected.

Global installation
^^^^^^^^^^^^^^^^^^^

Install the plugin globally so that it is accessible to all projects::

  npm install truffle-security

If you install MythX for Truffle in this manner, **you will in addition need to edit each project's configuration file** (``truffle-config.js``) to add the necessary plugin:

.. code-block:: javascript

   module.exports = {

     // ... 
 
       plugins: [ "truffle-security" ],
 
     // ... 

   };

Running
-------

To run MythX for Truffle, run the following command in the root of your configured Truffle project::

  truffle run verify

.. note:: The project must compile successfully in order for the plugin to run. If the project hasn't been compiled yet, MythX for Truffle will try to compile it first.

By default, all contracts in the project will be analyzed. To analyze only some of the contracts, append them to the command::

  truffle run verify MyContract MyContract2

The above command will analyze only the ``MyContract`` and ``MyContract2`` contracts.


Command options
---------------

To see the various command options available to you, run the following::

  truffle run verify --help

``--all``
^^^^^^^^^

Compile all contracts. Without this, only the contracts changed since last compile will be recompiled.

``--debug``
^^^^^^^^^^^

Provide additional debug output. Use ``--debug=2`` for more verbose output. Implies ``--no-progress``.

``--initial-delay <N>``
^^^^^^^^^^^^^^^^^^^^^^^

Minimum amount of time (in seconds) to wait before attempting a first status poll. Default is 45 seconds. `Read more about improving polling response <https://github.com/ConsenSys/armlet#improving-polling-response>`_.

``--json``
^^^^^^^^^^

Dump results in unprocessed JSON format. This disables providing any es-lint style reports. See also ``--yaml``.

``--limit <N>``
^^^^^^^^^^^^^^^

Limit the number of parallel analysis requests to no more than ``<N>``. As results come back, remaining contracts are submitted. The default and mamximum is 4, but this can be set lower.

``--min-severity <LEVEL>``
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ignore SWCs below the designated severity level. Options are ``warning`` or ``error``.

``--mode <MODE>``
^^^^^^^^^^^^^^^^^

Perform ``quick`` or in-depth (``full``) analysis.

``--no-color``
^^^^^^^^^^^^^^

Disable output coloring.

``--no-progress``
^^^^^^^^^^^^^^^^^

Disable progress bars during analysis.

``--style <STYLE>``
^^^^^^^^^^^^^^^^^^^

Output the report in the given `es-lint <https://eslint.org/docs/user-guide/formatters/>`_ style. Options include ``stylish``, ``json``, ``table``, ``tap``, ``unix``, and ``markdown``.

``--swc-blacklist <LIST>``
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ignore a specific SWC or list of SWCs. Use the number only (``107`` instead of ``SWC-107``). If using a list, use commas and no spaces to separate the SWCs (``103,111,115``).

``--timeout <N>``
^^^^^^^^^^^^^^^^^

Limit MythX analyses time to ``<N>`` seconds. The default is 300 seconds.

``--uuid <UUID>``
^^^^^^^^^^^^^^^^^

*(Experimental)* Display results from a prior analysis with the given UUID. Result is in YAML.

``--version``
^^^^^^^^^^^^^

Show package and MythX version information.

``--yaml``
^^^^^^^^^^

Dump results in unprocessed YAML format. This disables providing any es-lint style reports. See also ``--json``.


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