Quick Start
===========

- Documentation: `https://docs.cloud-deploy.io/ <https://docs.cloud-deploy.io/>`_
- Related repositories: `Claranet Github <https://github.com/claranet?utf8=%E2%9C%93&q=cloud-deploy&type=&language=>`_
- Cloud Deploy CLI: `Casper <https://github.com/claranet/casper>`_

.. figure:: https://www.cloudeploy.io/ghost/full_logo.png

Introduction
------------

Cloud Deploy (Ghost Project) aims to deploy applications in the Cloud, in a secure and reliable way.
Current version supports only AWS.

Key Features:
_____________

  * Developed in Python.

  * Designed for continuous deployment.

  * Create, configure and update AWS EC2 instances.

  * Used to deploy customer application code.

  * Cloud Deploy core is built with a REST API that any REST client can use.

  * A :ref:`ui`, available only for Claranet customers or with Enterprise license.

  * A :ref:`cli`


Application
-----------

It's the client code and all the requirements to set up on the instance.
Working in separate environments is one of major feature. Each ``application``
is identified by it's **name**, **env** and **role**.


Parameters
__________

An application is define by:

  * The AWS characteristics (in which region the application must be deployed,
    its instance type, VPC...)
  * The AutoScaling parameters (number of instances, minimum/maximum)

  * The instance specifications (number and size of the disks, the ssh key to
    associate, the security group to associate,...)

  * The mails to receive the deployment notifications.

  * Their features (a feature is the application requirement which will be
    installed on the EC2 instances. For example: PHP 5.4, Zabbix Agent, Nginx,
    PHP5-CURL)

  * Their modules(a module represent the code to deploy with some actions to
    realized before or/and after the code deployment. The code is system
    (example: Apache configuration's files) or client(the "pure" client
    application code)).

For more information, please refer to :ref:`application` page.

Jobs
----

Applications have several available job commands. A ``command`` can be operated on any existing application.
For each command, you can view the logs in real time.

For more information, please refer to :ref:`job` page.

Commands
________

  * ``Deploy``: To make a new deployment of an application module.

  * ``BuildImage``: create a new AMI with all the features defined in the
    application menu (Example: Launch a new instance and set up Apache and
    finally create a new AMI)

  * ``ReDeploy``: aka **rollback** To redeploy a previous version of an application module.

  * ``CreateInstance``: create a new EC2 instance based on the AMI create by the
    ``BuildImage`` command.

  * ``DestroyInstance``: Terminate the EC2 instance linked to the application.


For more information, please refer to :ref:`commands` page.
