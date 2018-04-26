.. _container:

.. title:: Deployment with buildpack step isolated in a container

Deployment with buildpack step isolated in a container
======================================================

.. toctree::
    :maxdepth: 2


Concept
*******

Before introducing this concept, the understanding of the buildpack step of the deployment workflow is required: cf :ref:`scripts` page.

The buildpack deployment in a container isolates the module deployment artifact building phase from the local system.

Why do we need to isolate that build?
*************************************

Applications have thirdparty dependencies requirements: for example Cloud Deploy depends on a list of python modules which are defined in ``requirements.txt``.

We execute this build in a container to prevent any conflict between the local system and build environments.

To do that, we have added steps in the initial deployment workflow.


**Cloud Deploy additional workflow steps**

**Build image**

1. When the ``buildimage`` of an AWS AMI is completed, an LXC container is launched, selected by its ``OS type`` and ``OS family``.
2. In that container, the ``features`` formulas and ``post/pre buildimage`` lifecycle hooks are applied.
3. When those steps are completed in the container, an image is taken and is stored in the local registry, aliased with the corresponding job ID.
4. This alias is then stored in the Cloud Deploy application to use it as a reference container for future deployments.
5. The container is destroyed.

Note: Container image retention is matched to AMI retention, i.e. each AWS AMI has its corresponding LXC image.

**Deployment**

1. Set a buildpack script in the Cloud Deploy application's module.
2. If the buildpack is set, a container is launched from the image in the local registry selected by its alias (i.e. the last successful buildimage job ID).
3. A container profile is created, and the module's path is mounted inside it.
4. The buildpack script is executed inside the container.
5. The container is destroyed.

How to enable buildpack in container
************************************

**System requirements**

1. Cloud Deploy installed on:

    * Debian >= 9 (Stretch) to install LXD with snapd because LXD is not available on debian natively
    * Ubuntu >= 16.04 LTS (The Xenial Xerus) to install LXD on stable canonical system

2. LXD installed via ``apt`` on Ubuntu or via ``snapd`` on Debian.
3. LXD daemon run with ``lxd`` group.
4. ``ghost`` user added to the ``lxd`` group.

**Configuration**

1. A container image source needs to be selected in the Build Infos section of the Cloud Deploy application.

    * All source images are available on a private registry. You can override this registry endpoint in the ``config.yml`` file.

2. ``container_debug`` can be enabled in ``config.yml`` to understand what's happening under the hood during ``buildimage`` and ``deployment`` steps (containers are not terminated).
