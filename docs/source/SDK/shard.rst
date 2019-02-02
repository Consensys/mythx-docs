Golang Library
==============

Shard is a lightweight Golang CLI for MythX. It serves as a reference
implementation.


Installation (unstable)
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

    $ snap install --devmode --edge shard


Configuration
^^^^^^^^^^^^^

You can put a config file in `$HOME/.config/.shard.yaml` containing your API
key. `shard.yaml` contains:

.. code-block:: yaml

    api-key: <put your api key here>

This way you don't have to put it in the CLI every time. Alternatively shard
also looks in the current directory for a configuration file if it can't find
one in the aforementioned directory.


Using Shard
^^^^^^^^^^^

As any with any tool, the help command can be very useful

.. code-block:: console

    $ shard
    Shard is a MythX light client

    Usage:
    shard [command]

    Available Commands:
    analyze     Analyzes the contract
    help        Help about any command
    version     Print the version number of Shard

    Flags:
    -k, --api-key string   The api key to authenticate with. Overrides config value.
        --config string    config file (default is $HOME/.config/.shard.yaml)
    -h, --help             help for shard
    -v, --verbose          Enable verbose logging.

    Use "shard [command] --help" for more information about a command.

To analyze a contract execute:

.. code-block:: console

    $ shard analyze 0x606b...
