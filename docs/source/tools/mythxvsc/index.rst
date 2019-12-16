.. meta::
   :description: MythXvsc is an extension for running MythX smart contract analysis from your favourite IDE.

.. _tools.mythxvsc:

MythXvsc
============================

MythXvsc is an extension for running MythX smart contract analysis from your favourite IDE.

The extensions provides:

- Smart contract compilation (via solidity VSCode extension)
- Log in to MythX platform
- AST extraction from compiled source
- Submission of analysis
- Displaying analysis result in VSCode in a linting fashion




Dependencies
-----

The MythXvsc extension depends on Juan Blanco’s solidity extension_. Make sure to download this from Visual Studio Code Marketplace before installing MythXvsc.

.. _extension: https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity

Installation
-----

Install from the Visual Studio marketplace here_.

.. _here: https://marketplace.visualstudio.com/items?itemName=mirkogarozzo.mythxvsc

Setup
-----
After installing the extension please enter your registered MythX ethAddress and password in VSCode user settings. These fields are properties of MythXvsc as shown in the screenshots below:

.. image:: installation.png
.. image:: user_settings.png

**Please note that the credentials stored this way are exposed to VSCode. Be sure to understand the security risk this entails or contact the extension developers if you don't. We are working on a more robust log-in implementation via a single-token.**

If no ethAddress and password provided the extension will fallback to use default trial credentials for MythX.

Usage
-----

Now simply open a ‘.sol’ file from inside a folder or workspace, and click on the MythX Analyze Smart Contract button that you will see in the top right of your IDE window. Otherwise right click with your mouse on the contract name and you will see the Analyze command.

.. image:: button_mythx.png
.. image:: right_click.png

Once the solidity compilation is done, you will be asked to pick a contract from a dropdown list of contracts that exist in the compiled ast. Please make sure to pick the main contract to avoid inconsistent results. 

.. image:: contract_picker.png

Now you can just sit back and wait for MythX to do its magic :) Once the analysis is over, you will see your smart contract issues highlighted in your code. This should take no longer than three minutes.

.. image:: finished_analysis.png
