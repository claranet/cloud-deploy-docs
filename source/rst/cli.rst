.. _cli:

Casper: CLI client
==================

.. toctree::
    :maxdepth: 2


Casper is a command line tool that interacts with Cloud Deploy (Ghost project).

Installation
------------
With `pip <https://pip.pypa.io>`_ (in a `virtualenv <https://virtualenv.pypa.io>`_ or not)

.. code-block:: shell

    pip install git+ssh://bitbucket.org/morea/casper

Usage
-----
Usage documentation is embedded in command.

.. code-block:: shell

    casper --help

Configuration
-------------
Location and credentials to access the Cloud Deploy instance are prompted if needed.

Configuration details can also be specified in a ``.casper`` configuration file.
The command will look for this file in the current directory and the user home directory, in this order.
Also, the configuration file can be specified with the ``--config-file`` option.

The configuration file can contain many profiles, the default one is named ``default`` and is mandatory. The profile can be chosen with the ``--profile`` option.

Here is an example of a configuration file.

.. code-block:: ini

    [default]
    endpoint=https://my_instance.cloudeploy.io
    username=casper

    [customer_x]
    endpoint=https://customer-x.cloudeploy.io
    username=casper
    password=XXXXXX

Any missing information for a profile will be prompted.
