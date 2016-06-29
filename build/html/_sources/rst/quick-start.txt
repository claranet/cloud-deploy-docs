Quick Start
===========

Introduction
------------

Ghost aims to deploy, in a secure and reliable way, applications in the Cloud.
Actual version support only AWS .

Ghost Features
______________

  * Developed in Python.

  * For continuous deployment.

  * Create, configure and update AWS EC2 instances.

  * Used to deploy client application code

  * Ghost core build within a REST API that any REST client could use it

  * A :ref:`ui`

  * A :ref:`cli`

The Ghost API is the core of this tool. Different elements compose this API


Application
-----------

Its the client code and all the requirements to set up on the instance.
Working is separate environment is one of major feature. Each ``application``
is identified with it's **name**, **env** and **role**.


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

Applications has several available job commands. A ``command`` will be operated
against an application already created. For each commands you can view the logs
in real time.

For more information, please refer to :ref:`job` page.

Commands
_________

  * ``Deploy``: To make a new deployment of an application module.

  * ``BuildImage``: create a new AMI with all the features defined in the
    application menu (Example: Launch a new instance and set up Apache and
    finally create a new AMI)

  * ``ReDeploy``: aka **rollback** To make a deployment of a previous version
    of an application module.

  * ``CreateInstance``: create a new EC2 instance based on the AMI create by the
    ``BuildImage`` command.

  * ``DestroyInstance``: Terminate the EC2 instance linked to the application.


For more information, please refer to :ref:`commands` page.
