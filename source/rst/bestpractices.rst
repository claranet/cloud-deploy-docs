.. _bestpratices:

Ghost Best Practices
====================

.. toctree::
    :maxdepth: 2


Introduction
------------

This documentation aims to provide data about what can be done with Ghost scripts.
In complement, please refer to the :ref:`commands` documentation.

Buildpack
---------

Buildpack overview
******************

The first buildpack step is to clone the git repository in a local directory before any upload on each host.
Please note that the "git clone" step is programmatically executed by Ghost, no need to write it in any user script.
The buildpack user script begins just after the "git clone" step.
The current directory will be set to the root of the git cloned repository.

Buildpack script overview
*************************

The buildpack script is used to install all external dependencies in the application directory.
After the buildpack script execution, the application directory will be compressed to be copied to each host, it should be as close as the target application filesystem.

Buildpack script prerequisites
******************************

This script is executed once on the Ghost instance during each deployment so any non local installation will be lost by the compression operation.
For example, global packages installation, like apt or yum packages won't be kept whereas local composer, pip, npm, gem installations will be kept in the archive.
Use this script to execute all commands that have a high execution cost and any external calls.

Pre-deploy
----------

Pre-deploy overview
*******************

The pre-deploy step copies the application directory modified by the buildpack script on each deployed hosts.
Copy and extraction step are programmatically executed by Ghost, no need to write them in any user script.
The pre-deploy user script begins just after the extraction step.
During pre-deploy, the soon-to-be-deployed sources are in a /ghost/ subdirectory which will be symlinked to the target directory at the deploy step.
The current directory will be set to the the root directory of the extracted copied directory.

Pre-deploy script overview
**************************

The pre-deploy script is used to do every mandatory operations before the symbolic link creation.
It will be executed locally on each hosts.
During the pre-deploy script execution, the previous code is still operational, the soon-to-be-deployed sources are in another directory.
After the pre-deploy script execution, the target symlink is changed to point to the new copy directory, the new sources are ready to run.

Pre-Deploy script prerequisites
*******************************

This script must not depend on external resources :
 - no internet call
 - no package install (apt-get, npm, pip, yum, gem, composer)
 - no downloads except from AWS S3

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
The post-deploy execution current directory is the Ghost application target directory.

Post-Deploy Requirements
************************

This script must not depend on external resources :
 - no internet call
 - no package install (apt-get, npm, pip, yum, gem, composer)
 - no downloads except from AWS S3

Keep in mind
------------

When autoscaling up, starting instances will only execute pre and post-deploy scripts.
Buildpack user script with costlier commands and external calls is only executed once on the Ghost instance to reduce risks of inconsistency between host deployments and permit faster new instance creation on autoscale up.
As external networking could be restricted or unavailable on deployed hosts, it is strongly advised against to use external network to install of download during pre-deploy or post-deploy user scripts.
