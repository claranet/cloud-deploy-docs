.. _container:

.. title:: Deployment With Buildpack Execution in Container

Deployment With Buildpack Execution in Container
================================================

.. toctree::
    :maxdepth: 2


Concept
*******

Before introducing this concept, the understanding of the buildpack step of the deployment workflow is required: cf :ref:`scripts` page.

The buildpack deployment in a container isolates the module deployment artifact building phase from the local system.

Why do we need to isolate that build?
*************************************

Applications have thirdparty dependencies requirements: for example Ghost depends on a list of python modules which are defined in ``requirements.txt``.

We execute this build in a container to prevent any conflict between the local system and build environments.

To do that, we have added steps in the initial deployment workflow.


**Ghost additional workflow steps**

**Build image**

1. When the ``buildimage`` of an AWS AMI is completed, an LXC container is launched, selected by its ``OS type`` and ``OS family``.
2. In that container, the ``features`` formulas and ``post/pre buildimage`` lifecycle hooks are applied.
3. When those steps are completed in the container, an image is taken and is stored in the local registry, aliased with the corresponding job ID.
4. This alias is then stored in the Ghost application to use it as a reference container for future deployments.
5. The container is destroyed.

Note: Container image retention is matched to AMI retention, i.e. each AWS AMI has its corresponding LXC image.

**Deployment**

1. Set a buildpack script in the Ghost application's module.
2. If the buildpack is set, a container is launched from the image in the local registry selected by its alias (i.e. the last successful buildimage job ID).
3. A container profile is created, and the module's path is mounted inside it.
4. The buildpack script is executed inside the container.
5. The container is destroyed.

How to enable buildpack in container
************************************

**System requirements**

1. LXD installed.
2. LXD daemon run with ``lxd`` group.
3. ``ghost`` user added to the ``lxd`` group.

**Configuration**

1. A container needs to be selected in the Build Infos section of the Ghost application.
2. ``container_debug`` can be enabled in ``config.yml`` to understand what's happening under the hood during ``buildimage`` and ``deployment`` steps (containers are not terminated).
