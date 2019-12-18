.. meta::
   :description: MythXvsc is an extension for running MythX smart contract analysis from VS Code. 
   
.. _tools.mythxvsc:

VS Code
=======

MythXvsc is an extension for running MythX smart contract analysis from your VS Code.

The extension provides:

- Smart contract compilation (via solidity VSCode extension)
- Log in to MythX platform
- AST extraction from compiled source
- Submission of analysis
- Displaying analysis result in VSCode in a linting fashion




Dependencies
------------

The MythXvsc extension depends on the `Solidity extension`_ by Juan Blanco. Make sure to download this from Visual Studio Code Marketplace before installing MythXvsc.

.. _Solidity extension: https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity

Installation
------------

Install_ from the Visual Studio marketplace.

.. _Install: https://marketplace.visualstudio.com/items?itemName=mirkogarozzo.mythxvsc

Setup
-----
After installing the extension please enter your registered MythX Ethereum Address and password in VSCode user settings. These fields are properties of MythXvsc as shown in the screenshots below:

.. image:: installation.png
.. image:: user_settings.png

.. warning:: Please note that the credentials stored this way are exposed to VSCode. Be sure to understand the security risk this entails or contact the extension developers if you don't. We are working on a more robust log-in implementation via a single-token.

If no Ethereum Address and/or password are provided, the extension will fallback to use default trial credentials for MythX.

Usage
-----

Now simply open a ‘.sol’ file from inside a folder or workspace, and click on the MythX Analyze Smart Contract button that you will see in the top right of your IDE window. Otherwise right click with your mouse on the contract name and you will see the Analyze command.

.. image:: button_mythx.png
.. image:: right_click.png

Once the solidity compilation is done, you will be asked to pick a contract from a dropdown list of contracts that exist in the compiled AST. Please make sure to pick the main contract to avoid inconsistent results. 

.. image:: contract_picker.png

Once the analysis is over, you will see your smart contract issues highlighted in your code. This should take no longer than three minutes.

.. image:: finished_analysis.png
