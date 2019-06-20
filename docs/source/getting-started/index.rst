.. _getting-started:

Getting Started
===============

This page will show how to start using MythX in the shortest number of steps.

Quickstart
----------

The quickest way to see MythX in action is by using a MythX tool such as the :ref:`MythX for Truffle <tooling.truffle>` plugin.

No registration is required for this, though the results will be limited. See the section on :ref:`using MythX for Truffle <tooling.truffle>` for more details.

#. In a terminal, navigate to the root of your local Truffle project.

#. Install the MythX plugin:

     .. code-block:: console

        npm install truffle-security

#. Analyze all the contracts in the project with MythX:

     .. code-block:: console

        truffle run verify

This will run a security analysis in Trial Mode, which limits the returned results to three vulnerabilities only. For a more complete report, you will need to create an account with MythX.


Creating an account
-------------------

To get the full functionality of MythX, you need to create an account.

.. note:: MythX requires `MetaMask <https://metamask.io>`_, a browser-based wallet application, in order to create accounts. You must be logged in to MetaMask before continuing. The active address will be associated with your account and be used for any plans you may purchase.

#. Go to https://mythx.io and slick the :guilabel:`Sign Up` button on the top right.

#. Fill out the registration form. You will need to supply a valid email address.

   .. image:: img/registration.png

#. When finished, click :guilabel:`Complete Registration`.

#. A MetaMask popup will display, asking for confirmation. Click :guilabel:`Sign` to continue.

   .. image:: img/metamasksignup.png
      :width: 50%

#. An API key will be generated for you and displayed. Please copy this key down, as you will not be able to retrieve it later. (You can generate a new one in your account dashboard if necessary.)

   .. image:: img/apikey.png
      :width: 50%

#. You will be sent an email to verify your address. You will need to verify your email address before you can use the MythX service.

   .. Verify this

Linking your account with tools
-------------------------------

Your account, once verified, is on the Free plan. This means that you can receive the complete report of vulnerabilities when running scans.

.. note:: MythX offers both free and paid plans. For information on plans and features, please see our `Plans <https://mythx.io/plans/>`_ page.

If using one of the :ref:`tools`, you will need to link your account to the tool to take advantage of your account's plan.

While the specifics of each tool differ, most tools will pick up your account information when stored in your system's environment variables.

.. list-table::
   :header-rows: 1

   * - Environment variable
     - Value
   * - ``MYTHX_ETH_ADDRESS``
     - Your MythX account (Ethereum address)
   * - ``MYTHX_PASSWORD``
     - API key supplied to you during registration

Please see :ref:`the specific page for your tool <tools>` to see more details about linking your account.
