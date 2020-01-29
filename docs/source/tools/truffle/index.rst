.. meta::
   :description: Run security analysis directly from your Truffle development environment with the MythX plugin. Learn how to run security analysis directly from your Truffle dev environment.

.. _tools.truffle:

Truffle integration with MythX
==============================

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

  npm install -g truffle-security

If you install MythX for Truffle in this manner, **you will in addition need to edit each project's configuration file** (``truffle-config.js``) to add the necessary plugin:

.. code-block:: javascript

   module.exports = {

     // ... 
 
       plugins: [ "truffle-security" ],
 
     // ... 

   };
   
Accounts and access
-------------------

You need to sign up for a MythX account in order to use the MythX plugin for Truffle. Your account, once verified, is on the Free plan. This means that you can receive the complete report of vulnerabilities when running scans.

MythX offers both free and paid plans. For information on plans and features, please see our `plans <https://mythx.io/plans/>`_ page. Truffle will pick up your account information when stored in your system's environment variables.


.. list-table::
   :header-rows: 1

   * - Environment variable
     - Value
   * - ``MYTHX_API_KEY``
     - JWT Token
   * - ``MYTHX_USERNAME``
     - Your MythX Email address
   * - ``MYTHX_PASSWORD``
     - Your MythX password
   * - ``MYTHX_ETH_ADDRESS``
     - Your MythX account (Ethereum address)


Authentication
--------------

Once your account is set up, head over to the `dashboard <https://dashboard.mythx.io/>`_.
In the *Profile* and *Tools* sections, various means of authentication are presented.

Using API Token (Recommended)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This is the recommended way of authenticating with the MythX smart contract analysis API. In the *Tools* section of your dashboard, there is an element labeled "MythX API Key". To generate a new API key, the account password must be entered:

.. image:: img/api-key-password.png

On successful authentication, a new JWT token is generated, which can be used for further authentication by API clients. It will only be shown once and can be copied using the icon on the right of the truncated secret string. If the token is lost, a new one can be generated again in the same way as explained above.

.. image:: img/api-key.png

This key can be passed to the MythX Security tool as an environment variable ``MYTHX_API_KEY``.

* **Linux / macOS**:

  .. code-block:: console

     export MYTHX_API_KEY=‘put your API key here!’

* **Windows**:

  .. code-block:: console

     set MYTHX_API_KEY=‘put your API key here!’
     
They API key can also be passed as a command line argument using ``—apiKey`` 

  .. code-block:: console

     --apiKey {‘put your API key here’}
     
     
Using Username and Password
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Alternatively, username and password can be used for authentication. This is not recommended, as a potential attacker can get access to your MythX account if these credentials are leaked. 

The Username corresponds to the MythX email address the account has been registered under, and the password is the one that has been set during registration, or separately in the MythX dashboard. Both can be passed by setting the ``MYTHX_USERNAME`` and ``MYTHX_PASSWORD`` environment variables.

You can temporarily add these environment variables to your terminal with the following commands (which will need to be customized with your account information):

* **Linux / macOS**:

  .. code-block:: console

     export MYTHX_USERNAME='your Mythx account’s email address'
     export MYTHX_PASSWORD='Put your password in here!'

* **Windows**:

  .. code-block:: console

     set MYTHX_USERNAME='your Mythx account’s email address'
     set MYTHX_PASSWORD='Put your password in here!'
     
     
Using ETH Address and Password (Not recommended)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Lastly, ETH Address and password can be used for authentication. This authentication method is also not recommended, as a potential attacker can get access to your MythX account as a whole if these credentials are leaked. In order to authenticate using ETH Address, you will need to link your MythX account to your Ethereum account through the *Profile* section of the dashboard. For compatibility reasons, this functionality has been included, however it is to be expected that this API feature will be disabled in the future.

The ETH Address corresponds to the Ethereum address associated with your MythX account, and the password is the one that has been set during registration, or separately in the MythX dashboard. Both can be passed by setting the ``MYTHX_ETH_ADDRESS`` and ``MYTHX_PASSWORD`` environment variables.

You can temporarily add these environment variables to your terminal with the following commands (which will need to be customized with your account information):

* **Linux / macOS**:

  .. code-block:: console

     export MYTHX_ETH_ADDRESS=‘your Mythx account’s Ethereum address'
     export MYTHX_PASSWORD='Put your password in here!'

* **Windows**:

  .. code-block:: console

     set MYTHX_ETH_ADDRESS=‘your Mythx account’s Ethereum address'
     set MYTHX_PASSWORD='Put your password in here!'


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

Options
-------

To see the various command options available to you, run the following::

  truffle run verify --help

You can pass options to the tool in two ways:

* Command line options (``--option``)
* Configuration file (``truffle-security.json``)

Command line options take precedence over any options specified in the configuration file.


Command line options
--------------------

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
Output results in unprocessed JSON format. Differs from ``--style=json`` which provides an es-lint compatible output format. See also ``--yaml``.

``--limit <N>``
^^^^^^^^^^^^^^^
Limit the number of parallel analysis requests to no more than ``<N>``. As results come back, remaining contracts are submitted. The default and mamximum is 4, but this can be set lower.

``--min-severity <LEVEL>``
^^^^^^^^^^^^^^^^^^^^^^^^^^
Ignore SWCs below the designated severity level. Options are ``warning`` or ``error``.

.. note:: Currently, the only severity levels are ``warning`` and ``error``, so choosing ``warning`` here has no effect (ignores nothing). Future versions may add support for an ``info`` severity level, which would be ignored.

``--mode <MODE>``
^^^^^^^^^^^^^^^^^
Perform ``quick``, ``standard``, or ``deep`` analysis. Refer to the `plans <https://mythx.io/plans/>`_ page to see which plan you need for each mode. 

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
Output results in unprocessed YAML format. Differs from ``--style=yaml`` which provides an es-lint compatible output format. See also ``--json``.

``--mythx-logs`` ``--no-mythx-logs``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Enable/disable MythX logs.

``--ci``
^^^^^^^^
Blocking non zero return for CI integrations to throw an error (non-zero exit code).

``--ci-whitelist { 101 | 103,111,115 | ... }``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
List of allowed SWCs that will not throw an error (non-zero exit code).

``--apiKey {api key generated from profile dashboard}``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Authenticate with api key instead of login details.

Configuration file
------------------

In addition to command line options, you can specify a configuration file named ``truffle-security.json``. Placed in the root of the project, this file can contain a list of options and values. Every option available on the command line is available here.

An example format of this file is as follows:

.. code-block:: json

   {
     "style": "table",
     "mode": "quick",
     "min-severity": "warning",
     "swc-blacklist": [103,111]
   }

For arguments that don't take a value (such as ``no-progress``) use the format:

.. code-block:: json
  
   {
     "no-format": true
   }

For arguments that take a list (such as ``swc-blacklist``), brackets for the values are optional.

.. note:: Command line options take precedence over any options specified in the configuration file.


.. seealso::

  * `MythX for Truffle (npm) <https://www.npmjs.com/package/truffle-security>`_
  * `MythX for Truffle (GitHub) <https://github.com/consensys/truffle-security>`_  
