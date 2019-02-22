JavaScript Library
==================

Armlet is a thin wrapper around the `MythX API <https://mythx.io/v1/openapi>`_ written in JavaScript which simplifies interaction with MythX.
For example, the library wraps API analysis requests into a promise.


Installation
------------

Just as with any nodejs package, install with:

.. code-block:: console

  $ npm install armlet


Example
-------

Here is a small example of how you might use this client. For
demonstration purposes, we'll set the credentials created on the
MythX, you can use either the Ethereum address or email
used during registration and the password you created:

.. code-block:: console

  $ export MYTHX_PASSWORD=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  $ # Only one of two below is needed:
  $ export EMAIL=me@example.com
  $ export MYTHX_ETH_ADDRESS=0x.............

Then to get the MythX analysis results with the promise returned by
the exposed function:

.. code-block:: javascript

  const armlet = require('armlet')
  const client = new armlet.Client(
    {
        password: process.env.MYTHX_PASSWORD,  // adjust this
        // Use one of the two options below
        ethAddress: process.env.MYTHX_ETH_ADDRESS,
        email: process.env.EMAIL  // adjust this
    })
  const data = {
    contractName: 'TestMe',
    abi: [
      {
        constant: false,
        inputs: [
          {
            name: 'first_input',
            type: 'uint256',
          },
        ],
        name: 'lol',
        outputs: [
          {
            name: '',
            type: 'uint256',
          },
        ],
        payable: false,
        stateMutability: 'nonpayable',
        type: 'function',
      },
    ],
    bytecode: '0xf6...',
    deployedBytecode: '0xf6...',
    sourceMap: '25:78:1:-;;;;8:9:-1;5:2;;;30:1;27;20:12;5:2;25:78:1;;;;;;;',
    deployedSourceMap: '25:78:1:-;;;;8:9:-1;5:2;;;30:1;27;20:12;5:2;25:78:1;;;;;;;',
    sourceList: [
      'basecontract.sol',
      'maincontract.sol',
    ],
    sources: {
      'basecontract.sol': {
        source: '[... source code ...]',
      },
      'maincontract.sol': {
        source: '[... source code ...]',
      },
    },
    analysisMode: 'full',
  };
  client.analyze({data})
    .then(issues => {
      console.log(issues)
    }).catch(err => {
      console.log(err)
    })


You can also specify the timeout in milliseconds to wait for the analysis to be
done (the default is 10 seconds). For instance, to wait up to 5 seconds:

.. code-block:: javascript

  client.analyze({data, timeout: 5000})
    .then(issues => {
      console.log(issues)
    }).catch(err => {
      console.log(err)
    })


.. seealso::

  * `npm package <https://www.npmjs.com/package/armlet>`_
  * `The GitHub project <https://github.com/consensys/armlet>`_
  * `MythX API spec <https://staging.api.mythx.io/v1/openapi/>`_
  * `MythX JS SDK <sdk/mythx-js-sdk>`_
