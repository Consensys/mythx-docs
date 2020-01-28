.. meta::
   :description: How to start using MythX in the shortest number of steps including creating your account with MetaMask and linking available API tools.

.. _getting-started:

Getting started with MythX security tools
=========================================

This page will show how to start using MythX in the shortest number of steps.

Creating an account
-------------------

To use MythX, you need to create an account.

#. Go to https://mythx.io and click the :guilabel:`Sign Up` button on the top right.

#. Fill out the registration form. You will need to supply a valid email address.

   .. image:: img/registration2.png
    :width: 50%
    
#. When finished, click :guilabel:`Complete Registration`.

#. A success message will show, indicating your account has been created successfully. You will be sent an email to verify your email address. 

   .. image:: img/success.png
      :width: 50%

.. note:: You can link your Ethereum account through `MetaMask <https://metamask.io>`_, a browser-based wallet application, by navigating to your *profile* section and clicking the "Link Ethereum Address" link. After you sign the request, the active address will be associated with your account and be used for any plans you may purchase using crypto.

   .. image:: img/metamask1.png
      :width: 50%
      
   .. image:: img/metamasksignup.png
    :width: 50%

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
   * - ``MYTHX_API_KEY``
     - JWT Token
   * - ``MYTHX_ETH_ADDRESS``
     - Your MythX account (Ethereum address)
   * - ``MYTHX_PASSWORD``
     - Password set during registration
     
Authentication
--------------

Once your account is set up, head over to the `dashboard <https://dashboard.mythx.io/>`_.
In the *Profile* section, various means of authentication are presented.


Using API Tokens
~~~~~~~~~~~~~~~~

This is the recommended way of authenticating with the MythX smart contract
analysis API. In the *Profile* section there is an elements labeled "MythX API Key".
To generate a new API key, the account password must be entered:

.. image:: img/api-key-password.png

On successful authentication a new JWT token is generated, which can be
used for further authentication by API clients. It will only be shown once
and can be copied using the icon on the right of the truncated secret string.
If the token is lost, a new one can be generated again in the same way as
explained above.

.. image:: img/api-key.png

This key can be passed to the MythX Security tool as an environment variable :code:`MYTHX_API_KEY`.


Using Address and Password (not recommended)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Alternatively, username and password can be used for authentication.
This is not recommended as a potential attacker can get access to the MythX
account as a whole if these credentials are leaked.
For compatibility reasons this functionality has been included, however it
is to be expected that this API feature will be disabled in the future.

The username corresponds to the Ethereum address the MythX account has been
registered under, and the password is the one that has been set during
registration, or separately in the MythX dashboard.
Both can be passed by setting the
:code:`MYTHX_USERNAME` and :code:`MYTHX_PASSWORD` environment variables.

Note that if username and password, as well as an API token are given,
the API token will always take precedence and no login action using
the provided credentials will be performed.

Please see :ref:`the specific page for your tool <tools>` to see more details about linking your account.

