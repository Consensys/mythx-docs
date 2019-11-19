.. meta::
   :description: Learn how to install and use MythXJS, a JavaScript library for interacting with the MythX API for securing smart contracts.

.. _tools.mythxjs:

MythXJS Guide: Installation & Usage
===================================

`MythXJS <https://github.com/ConsenSys/mythxjs>`_ is a JavaScript library for interacting with the MythX API.


Installation
------------

MythXJS can be installed via ``npm``:

.. code-block:: console

   npm install mythxjs

Examples
--------

Creating a new instance of the library using ES6 modules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: javascript

   import { Client } from 'mythxjs'

   const mythx = new Client('0x0000000000000000000000000000000000000000', 'trial', 'testTool');

Performing a ``login`` request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: javascript

   // Logs in and returns an object containing access and refresh token
   const tokens = await mythx.login()

Submitting an analysis using bytecode only
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: javascript

   const bytecode = '0xfe'
   await mythx.submitBytecode(bytecode)


Getting a list of detected issues
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: javascript

   await mythx.getDetectedIssues('1111-2222-3333-4444')


Logging in with MetaMask
------------------------

In order to keep MythXJS as lean as possible it does not handle `MetaMask <https://metamask.io>`_ integration directly. Instead it provides two methods:

* ``getChallenge()``
* ``loginWithSignature()``

With these methods, you can handle the MetaMask integration as you prefer. You can also work with your preferred version of `web3`.


Here is an example using React and ``web3@1.0.0-beta.37``:

.. code-block:: javascript

    const handleSignMessage = (account, data) => {
        try {
            return new Promise((resolve) => {
                const {value} = data.message
                if (!account) {
                  console.error('no-account')
                }
                  const params = [account, JSON.stringify(data)]
                  web3.currentProvider.send(
                            { method: 'eth_signTypedData_v3', params, from: account },
                            (err, result) => {
                              if (err || result.error) {
                                console.error('Error with handling signature.', err)
                              }
                              resolve(value + '.' + result.result)
                            }
                        )
                }).catch((error) => {
                  console.error(error)
                })
        } catch(err) {
            console.error(err)
        }
    }

    const loginWithMM = async () => {
        const accounts = await web3.eth.getAccounts();
        const account = accounts[0]

        const data = await mythx.getChallenge(account.toLowerCase())
        
        handleSignMessage(account, data).then(
            async (message) => {
                // Returns set of tokens
                const result = await mythx.loginWithSignature(message)
                console.log(result, 'ress')
            }
        ).catch(err => console.error(err))
    }


.. seealso::

   * `MythXJS documentation (GitHub) <https://consensys.github.io/mythxjs/classes/_apiservices_clientservice_.clientservice.html>`_
   * `Source (GitHub) <https://github.com/ConsenSys/mythxjs>`_
   * `OpenAPI spec (MythX) <https://api.mythx.io/v1/openapi>`_
