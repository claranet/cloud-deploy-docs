.. _scripting:

Scripting - best practices
==========================

.. toctree::
    :maxdepth: 2


Introduction
------------

This documentation is here to give you all informations you need to know what you can do with Ghost scripts.
In complement, please refer to the :ref:`commands` documentation.

Buildpack overview
------------------

The first buildpack step is to clone the git repository in a local directory before upload it on each host.
Please note that "git clone" step is totally transparent so you don't have to add this step in your script.
Your buildpack script begins just after the "git clone" step.
Your current directory has been change to the root directory of your git repository code.

Buildpack script overview
-------------------------

The buildpack script is used to add all your externals dependencies in your source code.
After the buildpack script execution, we will compress your contents, at this step the local directory have to be as close as possible to the target directory.

Buildpack script prerequisites
------------------------------

This script have to execute all commands that have an high execution time cost and every calls to externals dependencies.
System packages install like apt-get or yum are forbidden.
Applicative packages install like composer (php), pip (python), npm (nodeJS), gem (ruby) are allowed.
These tools will work only if you use it locally. Global installs are restricted.

Pre-Deploy overview
-------------------

The role of Pre-Deploy step is to download your archive in a local directory of each hosts.
At this step, the directory of your script is in /ghost/<folders>. At the end of this script, the current directory will be symlink to the target directory.
Please note that "download" and "decompress" step are totally transparent so you don't have to add these steps in your script.
Your pre-deploy script begins just after the "download" and "decompress" step.
Your current directory has been change to the root directory of your code.

Pre-Deploy script overview
--------------------------

The predeploy script is used to do every mandatory operations before the symbolic link creation.
It will be execute locally on each hosts.
On the predeploy step, the path configured in your application is not altered, so your previous code continue to work as expected.
After the predeploy script execution, we will symlink the current directory to the target directory.
At this step, your previous code will be replaced by the new one.

Pre-Deploy script prerequisites
-------------------------------

This script must not depend on external resources :
 - no internet call
 - no package install (apt-get, npm, pip, yum, gem, composer)
 - no downloads except from AWS S3

Post-Deploy overview
--------------------

The role of Post-Deploy step is to create a symbolic link between the current repository and the path specified in your Ghost application.
Be careful, at this step, your code has changed in your application path directory.

Post-Deploy script overview
---------------------------

The postdeploy script is used to do final operations to have an available service.
It will be execute locally on each hosts.
It's often the step where you will implement your service reload or restart.
Your current directory is the path of your current Ghost application.

Post-Deploy Requirements
------------------------

This script must not depend on external resources :
 - no internet call
 - no package install (apt-get, npm, pip, yum, gem, composer)
 - no downloads except from AWS S3

Keep in mind
------------

When you use an autoscaling, some instances will start then execute all your modules pre-deploy and post-deploy.
Your buildpack script is execute only once, that's why you have to do the most operations in it then your service will be shortly available in the case of a new instance creation.
We cannot control repository updates and the availability of Internet and externals networks so to have a consistent application, you cannot use install and external calls on your predeploy and postdeploy.
