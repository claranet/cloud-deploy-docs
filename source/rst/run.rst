.. _run:

RUN: Debug your deployed instances
==================================

.. toctree::
    :maxdepth: 2

Introduction
------------

You may need to debug some failed deployments with Cloud Deploy.
There are two main cases you may have to debug on:

 - An error during a hot deployment (via the :ref:`cmd_deploy` command)
 - An error on a running instance, probably at first bootstrap

This section details most of the tips you need to know and which may help you debug those kind of cases.

Debug hot deployment
--------------------

When you trigger a :ref:`cmd_deploy` command a job is created on Cloud Deploy.
If an error occurs during this job, you will have the real time log to help you debug what happened.

Reminder:

 - The job log is available through the WebUI, via API and via CLI (with :ref:`cli`)
 - The job log file is also stored and available on the S3 bucket used by Cloud Deploy, with this path: ``/log/job/{job-id}.txt``
 - There are also some job logs available locally on Cloud Deploy, at ``/var/log/ghost/{job-id}.txt``

Keep in mind that you must follow our :ref:`bestpratices` to avoid unsuccessful deployments.

Debug instance bootstrap
------------------------

Even if all your module deployments were successful, it might happen that a new fresh instance
(created via :ref:`cmd_createinstance` command or created by the AutoScaling Group)
isn't well deployed. In that case, here is a bunch of elements you may use to debug your instance deployment.

Early bootstrap logs
********************

At first boot, `cloud-init <http://cloudinit.readthedocs.io/en/latest/>`_ configures the instance and triggers the `userdata <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html>`_ script.
You can check the cloud-init log in ``/var/log/cloud-init-output.log``.

If your instance cannot connect to the S3 bucket, you will see in this log some errors when cloud-init tries to download and run the Cloud Deploy bootstrap script (called ``stage2``).

.. warning:: Regarding internet connectivity issues, please check where is located your instance. It must be in a Subnet routed via an Internet Gateway (AKA "public subnet") or routed via a NAT Gateway (AKA "private subnet").

Here is an example of a log with a correct early bootstrap execution:

.. code-block:: sh

    $ cat /var/log/cloud-init-output.log
    Cloud-init v. 0.7.9 running 'init-local' at Tue, 07 Nov 2017 18:57:33 +0000. Up 14.32 seconds.
    Cloud-init v. 0.7.9 running 'init' at Tue, 07 Nov 2017 18:57:35 +0000. Up 16.92 seconds.
    [..]
    Generating locales (this might take a while)...
    en_US.UTF-8... done
    Generation complete.
    Cloud-init v. 0.7.9 running 'modules:config' at Tue, 10 Apr 2018 16:02:42 +0000. Up 19.41 seconds.
    + S3_BUCKET=s3.support.ghost-packages.eu-west-1
    + S3_REGION=eu-west-1
    ++ curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone
    + EC2_AVAIL_ZONE=eu-west-1b
    ++ sed -e 's:\([0-9][0-9]*\)[a-z]*$:\1:'
    ++ echo eu-west-1b
    + EC2_REGION=eu-west-1
    ++ which aws
    + AWS_BIN=/usr/local/bin/aws
    + '[' 0 -ne 0 ']'
    + LOGDIR=/var/log/ghost/
    + STAGE2_PATH=/var/lib/ghost/stage2_bootstrap
    + STAGE2_PATH_LOG=/var/log/ghost/stage2_bootstrap.log
    + '[' '!' -d /var/lib/ghost ']'
    + mkdir /var/lib/ghost
    + '[' '!' -d /var/log/ghost/ ']'
    + mkdir /var/log/ghost/
    + download_stage2
    + /usr/local/bin/aws s3 cp s3://s3.support.ghost-packages.eu-west-1/ghost/stage2 /var/lib/ghost/stage2_bootstrap --region eu-west-1
    download: s3://s3.support.ghost-packages.eu-west-1/ghost/stage2 to var/lib/ghost/stage2_bootstrap
    + chmod +x /var/lib/ghost/stage2_bootstrap
    + execute_stage2
    + /var/lib/ghost/stage2_bootstrap
    Cloud-init v. 0.7.9 running 'modules:final' at Tue, 10 Apr 2018 16:02:46 +0000. Up 23.81 seconds.
    Cloud-init v. 0.7.9 finished at Tue, 10 Apr 2018 16:02:56 +0000. Datasource DataSourceEc2.  Up 33.71 seconds


Cloud Deploy bootstrap logs
***************************

The ``stage2`` bootstrap script, stored at ``/var/lib/ghost/stage2_bootstrap`` (previously at ``/tmp/stage2`` with Cloud Deploy version < ``v17.09``)
will have its detailed execution log at ``/var/log/ghost/stage2_bootstrap.log`` (previously at ``/tmp/log_bootstrap_stage2.txt`` with Cloud Deploy version < ``v17.09``).

This script has a locking mechanism, it ensures that only one deployment is processed and any other concurrent deployment will have to wait for the lock to be released.
The lock path is located at ``/run/lock/ghost-stage-2``.

.. warning:: Don't try to manually lock or unlock if you don't need to. If your instance is locked, be sure that no deployment is in progress and then proceed to manually unlock via the command:

.. code-block:: sh

  $ sudo rmdir -v /run/lock/ghost-stage-2


If an error occurs during this script execution, you will be able to have the detailed execution stacktrace in the log file.
By running the command:

.. code-block:: sh

  $ tail -1 /var/log/ghost/stage2_bootstrap.log

you will have the execution status code. Please refer to :ref:`run_status_codes` to understand where the bootstrap script failed.


Per module deployment status and log
************************************

If you need to go deeper into your debugging, you can check every deployment logs which are stored at ``/var/log/ghost/{deployment-date}_deploy.txt``.

.. code-block:: sh

    $ ls -la /var/log/ghost/
    total 36
    drwxr-xr-x  2 root root  4096 Apr 25 13:50 .
    drwxr-xr-x 10 root root  4096 Jun 28 06:25 ..
    -rw-r--r--  1 root root  2745 Apr 10 16:02 20180410_160250_deploy.txt
    -rw-r--r--  1 root root  2301 Apr 25 13:50 20180425_135003_deploy.txt
    -rw-r--r--  1 root root 19370 Apr 10 16:02 stage2_bootstrap.log

You can also have the state of every modules deployed on the current instance by checking files at ``/var/lib/ghost/``.

.. code-block:: sh

    $ ls -la /var/lib/ghost/
    total 36
    drwxr-xr-x  2 root  root   4096 Apr 25 13:50 .
    drwxr-xr-x 25 root  root   4096 Apr 10 16:02 ..
    -rw-r--r--  1 root  root     88 Apr 25 13:50 www_succeed
    -rw-r--r--  1 root  root     91 Apr 25 14:42 test_failed

Each file is named following this convention: ``${MODULE_NAME}_${DEPLOYMENT STATUS}``, the latest modification date of the file is matching the latest deployment date for this module.
Each file contains the list of all the packages revision deployed for this module, with their absolute and unique path, ordered by date asc.
Here is an example:

.. code-block:: sh

    $ ls -la /var/www/
    total 8
    drwxr-xr-x  2 root root 4096 Apr 25 13:50 .
    drwxr-xr-x 12 root root 4096 Apr 10 16:02 ..
    lrwxrwxrwx  1 root root   43 Apr 25 13:50 html -> /ghost/529bf19a-99da-4f92-9afb-26f31fd2ef92

    $ cat -tne /var/lib/ghost/www_succeed
        1  /ghost/1b01c340-f448-4a31-a72b-011a2e3b689b$
        2  /ghost/529bf19a-99da-4f92-9afb-26f31fd2ef92$


.. _run_status_codes:

Deploy script status codes
--------------------------

Here is a detailed table with every possible status code returned by the deployment script and their description.

+-------------+---------------------------------------------------------------------------------------------------------------+
| Status code | Description                                                                                                   |
+=============+===============================================================================================================+
| 0           | No error, deployment successful                                                                               |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -1          | Cannot retrieve instance tags: might be an internet connectivity issue, or IAM role policy issue              |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -3          | Cannot download manifest file: might be an internet connectivity issue, or IAM role policy issue              |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -5          | Error during instance bootstrap life cycle hooks execution (see :ref:`scripts` for more details)              |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -10         | Error during a module deployment, please check the associated log for more details                            |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -11         | Cannot download (from the bucket) or extract the module archive (artifact)                                    |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -12         | Error during :ref:`reco_pre_deploy` hook execution, please check the associated log for more details          |
+-------------+---------------------------------------------------------------------------------------------------------------+
| -13         | Error during :ref:`reco_post_deploy` hook execution, please check the associated log for more details         |
+-------------+---------------------------------------------------------------------------------------------------------------+
