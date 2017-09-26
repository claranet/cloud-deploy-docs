.. _scripts:

Ghost Scripts
=============

.. toctree::
    :maxdepth: 2

Scripts
-------

Ghost enables you to launch custom scripts at every steps of the deployment and build process (bake image template).
Here is an overview and a description of thoses scripts.

    - **pre_buildimage**: Script executed in the `buildimage` command before formulas provisioning. It allows you to prepare the source AMI before the execution of all of your application's features formulas. It can be usefull in order to change package's mirrors location for example.

    - **post_buildimage**: Script executed in the `buildimage` command after formulas provisioning. You can tweak and install custom system packages after the features provisioning.

    .. figure:: /images/buildimage_workflow.png

    - **pre_bootstrap**: Script executed when a new instance starts, before the deployment of modules packages.

    - **post_bootstrap**: Script executed when a new instance starts, after the deployment of modules packages. It can be used to verify and validate the whole instance deployment.

    .. figure:: /images/bootstrap_workflow.png

    - **buildpack**: Script executed on Ghost when deploying a new version of a module (new package). This script will prepare the git repository before making the archive package which will be pushed on S3. Every external dependencies required by the application **must** be resolved in this script.

    - **pre_deploy**: Script executed on every instance when deploying a module package. This script will prepare the target instance *before* symbolic link swap. This script **must not** depend on external resources (no internet call, no package install, no downloads).

    - **post_deploy**: Script executed on every instance when deploying a module package. This script will prepare the target instance *after* symbolic link swap. This script **must not** depend on external resources (no internet call, no package install, no downloads).

    - **after_all_deploy**: Script executed on Ghost when deploying a new version of a module (new package). This script is executed after the package deployment on every instance of the current application.

    .. figure:: /images/deploy_workflow.png

.. _scripts_vars:

Environment variables
---------------------

When custom scripts and binaries are triggered in the Ghost deployment workflow, many variables are available in the environment to help you making generic scripts.
It's also possible to define custom variables which will be configured within the Ghost server environment and therefore available when running scripts over instances.

+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| Variables                   | Purpose                                  | pre_buildimage | post_buildimage | pre_bootstrap | post_bootstrap | buildpack | pre_deploy | post_deploy  | after_all_deploy | execute_script |
+=============================+==========================================+================+=================+===============+================+===========+============+==============+==================+================+
| GHOST_APP                   | Application name                         | ✔              | ✔               | ✔             | ✔              | ✔         | ✔          | ✔            | ✔                | ✔              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_ENV                   | Application environment                  | ✔              | ✔               | ✔             | ✔              | ✔         | ✔          | ✔            | ✔                | ✔              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_ENV_COLOR             | Application color if Blue/Green enabled  | ✔              | ✔               | ✔             | ✔              | ✔         | ✔          | ✔            | ✔                | ✔              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_ROLE                  | Application role                         | ✔              | ✔               | ✔             | ✔              | ✔         | ✔          | ✔            | ✔                | ✔              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_NAME           | Module name                              |                |                 |               |                | ✔         | ✔          | ✔            | ✔                | ~              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_PATH           | Module destination path                  |                |                 |               |                | ✔         | ✔          | ✔            | ✔                | ~              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_REPO           | Module git repository                    |                |                 |               |                | ✔         | ✔          | ✔            | ✔                | ~              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_REV            | Module git revision deployed             |                |                 |               |                | ✔         | ✔          | ✔            | ✔                |                |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_COMMIT         | Module git commit hash deployed          |                |                 |               |                | ✔         | ✔          | ✔            | ✔                |                |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_COMMIT_MESSAGE | Module git commit message                |                |                 |               |                | ✔         | ✔          | ✔            | ✔                |                |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| GHOST_MODULE_USER           | User who triggered the deployment        |                |                 |               |                | ✔         | ✔          | ✔            | ✔                | ✔              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+
| *custom var*                | Defined by user in Ghost App             | ✔              | ✔               | ✔             | ✔              | ✔         | ✔          | ✔            | ✔                | ✔              |
+-----------------------------+------------------------------------------+----------------+-----------------+---------------+----------------+-----------+------------+--------------+------------------+----------------+

