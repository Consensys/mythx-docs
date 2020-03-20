.. meta::
   :description: How to start using MythX in the shortest number of steps including creating your account with MetaMask and linking available API tools.

.. _getting-started:

Getting started with MythX security tools
=========================================

This page will show how to start using MythX in the shortest number of steps.

Creating an Account
-------------------

To use MythX, you need to create an account.

#. Go to https://mythx.io and click the :guilabel:`Sign Up` button on the top right.

#. Fill out the registration form. You will need to supply a valid email address.

   .. figure:: img/registration2.png
    :width: 50%
    
#. When finished, click :guilabel:`Complete Registration`.

#. A success message will show, indicating your account has been created successfully. You will be sent an email to verify your email address. 

   .. figure:: img/success.png
      :width: 50%

.. note::

   It is recommended that you link your Ethereum account to your profile as you will use this credential along with your password to access the MythX API via client tools such as Remix. This is done with `MetaMask <https://metamask.io>`_.

   .. figure:: img/metamask1.png

   Once linked, MetaMask will ask to sign a transaction to connect to MythX.
      
   .. figure:: img/metamasksignup.png
    :width: 50%

   .. Verify this


Linking your account with tools
-------------------------------

Your account, once verified, is on the Free plan.

.. note:: MythX offers both free and paid plans. For information on plans and features, please see our `Pricing <https://mythx.io/plans/>`_ page.

If using one of the :ref:`tools`, you will need to link your account to the tool to take advantage of your account's plan.

While the specifics of each tool differ, most tools will pick up your account information when stored in your system's environment variables.

.. list-table::
   :header-rows: 1

   * - Environment variable
     - Value
   * - ``MYTHX_API_KEY``
     - <Your API key>
    
MythX uses an API key for authentication. This API key can be generated in your `dashboard <https://dashboard.mythx.io/>`_. In the Profile tab there is a section titled :guilabel:`MythX API Key`. Generate a new API key by entering your account password:

.. figure:: img/api-key-password.png

On successful authentication, a new API key is generated, which can be used for further authentication by API clients. It will only be shown once, and can be copied using the icon on the right of the truncated secret string. If the token is lost, a new one can be generated again in the same way as explained above.

.. figure:: img/api-key.png

This key can be passed to MythX as an environment variable :code:`MYTHX_API_KEY`.

* **Linux / macOS**:

  .. code-block:: console

     export MYTHX_API_KEY='put your API key here!'

* **Windows**:

  .. code-block:: console

     set MYTHX_API_KEY='put your API key here!'

.. note:: Although using the API key is the recommended means of authentication, there are certain tools that do not yet support the API token (for example: :ref:`Remix <tools.remix>`). For these tools, you can authenticate via your Ethereum address or user name and password.

Please see :ref:`the specific page for your tool <tools>` to see more details about linking your account.

