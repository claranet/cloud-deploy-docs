.. _bestpratices:

Usage best practices
====================

.. toctree::
    :maxdepth: 2


Introduction
------------

This documentation aims to provide data about what can be done with Cloud Deploy scripts.
In complement, please refer to the :ref:`commands` documentation.


General guidance
----------------

Each script is running on Unix systems. If a shebang is present on the top of your script, it will be run with the specified interpreter program.
By example, this shebang will run the script with python program (if python is installed):

.. code-block:: none

  #!/bin/python

By default, Cloud Deploy will check the exit status of the entire script. If the exit status is equal to 0, the Cloud Deploy job status is ``success``. For others status, it will be ``failed`` status.
If your script language is bash, it is recommended to add a ``set -e`` command on the top of your script to cancel the script execution on exit status different of 0 and return a failed status to the Cloud Deploy job.

Buildpack
---------

Buildpack overview
******************

The first buildpack step is to clone the git repository in a local directory before any upload on each host.
Please note that the ``git clone`` step is programmatically executed by Cloud Deploy, no need to write it in any user script.
The buildpack user script begins just after the ``git clone`` step.
The current directory will be set to the root of the git cloned repository.

Buildpack script overview
*************************

The buildpack script is used to install all external dependencies in the application directory.
After the buildpack script execution, the application directory will be compressed to be copied to each host, it should be as close as the target application filesystem.

Buildpack script prerequisites
******************************

This script is executed once on the Cloud Deploy instance during each deployment so any non local installation will be lost by the compression operation.
For example, global packages installation, like apt or yum packages won't be kept whereas local composer, pip, npm, gem installations will be kept in the archive.
Use this script to execute all commands that have a high execution cost and any external calls.

Buildpack script example
************************

.. code-block:: sh

  #!/bin/bash

  set -x # display expanded instructions before execution
  set -e # exit on first error (non-zero status)

  php composer # trigger all command needed to build the php application
  bower # or any tool needed to minify, compile, prepare assets and code for deployment

  vault # or any password manipulation, injected in application configuration


Pre-deploy
----------

Pre-deploy overview
*******************

The pre-deploy step copies the application directory modified by the buildpack script on each deployed hosts.
Copy and extraction step are programmatically executed by Cloud Deploy, no need to write them in any user script.
The pre-deploy user script begins just after the extraction step.
During pre-deploy, the soon-to-be-deployed sources are in a ``/ghost/`` subdirectory which will be symlinked to the target directory at the deploy step.
The current directory will be set to the root directory of the extracted copied directory.

Pre-deploy script overview
**************************

The pre-deploy script is used to do every mandatory operations before the symbolic link creation.
It will be executed locally on each host.
During the pre-deploy script execution, the previous code is still operational, the soon-to-be-deployed sources are in another directory.
After the pre-deploy script execution, the target symlink is changed to point to the new copy directory, the new sources are ready to run.

Pre-deploy requirements
***********************

.. warning:: This script must not depend on external resources: no internet call, no package install, (apt-get, npm, pip, yum, gem, composer), no downloads except from AWS S3

Pre-deploy script example
*************************

.. code-block:: sh

  #!/bin/bash

  set -x # display expanded instructions before execution
  set -e # exit on first error (non-zero status)

  # clear cache
  # update queues
  # prepare to stop the current running application or service


Post-deploy
-----------

Post-deploy overview
********************

The post-deploy step is executed right after the target symlink change.
At this step, the new sources are ready to run.

Post-deploy script overview
***************************

The post-deploy script aims to activate the new sources.
It will be executed locally on each hosts.
Most scripts consist in service reloading/restarting.
The post-deploy execution working directory is the Cloud Deploy application target directory.

Post-deploy requirements
************************

.. warning:: This script must not depend on external resources: no internet call, no package install, (apt-get, npm, pip, yum, gem, composer), no downloads except from AWS S3

Post-deploy script example
**************************

.. code-block:: sh

  #!/bin/bash

  set -x # display expanded instructions before execution
  set -e # exit on first error (non-zero status)

  server xxx-xxx reload # Reload/restart of service

After all deploy
----------------

After all deploy overview
*************************

The After All Deploy script step is executed on the Cloud Deploy instance after execution of all pre and post deploy scripts.
 
After all deploy script overview
********************************

The script is executed on the Cloud Deploy then you can add an action at the end of the module deployment that you have to execute once.
Please keep in mind that your Cloud Deploy needs to have rights to do this action.

After all deploy script prerequisites
*************************************

No data will be sent to your application instances at this step.

After all deploy script example
*******************************

.. code-block:: sh

  #!/bin/bash

  set -x # display expanded instructions before execution
  set -e # exit on first error (non-zero status)

  # Deployment notification (NewRelic ?)
  # Load Balancer or external dependency notification
  # Database schema update


Keep in mind
------------

When the AutoScalingGroup scales up, starting instances will only execute pre and post-deploy scripts.
BuildPack user script with costlier commands and external calls is only executed once on the Cloud Deploy instance to reduce risks of inconsistency between host deployments and permit faster new instance bootstrapping on autoscale up.
As external networking could be restricted or unavailable on deployed hosts, it is strongly advised against to use external network to install of download during pre-deploy or post-deploy user scripts.

Scripts examples
----------------

Bash/Shell
**********

.. code-block:: sh

  #!/bin/bash
  
  set -x # enable instruction printing, useful for debugging
  set -e # exit on first error (non-zero status)

  ./code # script or code to execute
  my_command || exit 1 # to make sure to exit and stop the script if `my_command` fails
  my_command || echo "ok" # to continue the script even if `my_command` fails. Warning: not compatible with `set -e`

