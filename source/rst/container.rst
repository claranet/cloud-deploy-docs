.. _container:

.. title:: BuildPack Deployment With Container

BuildPack Deployment With Container
===================================

.. toctree::
    :maxdepth: 2


Concept
*******

Before to introduice this concept, you need to know the buildpack concept in deployment workflow : cf :ref:`scripts` page.

The buildpack deployment in a container makes possible to isolate the build of sources arfifact during a module deployment.

Why we need to isolate that build ?
***********************************

An application contains some packages dépencies: for exemple Ghost needs a list of python modules who are store in requirements.txt.

To be sure that packages didn't create conflicts with the Ghost instance, we need to execute this installation in a container.

To do that, we have added steps in the initial workflow deployment.


**Ghost additional Wordflow steps**

**Build image**


1. When the build images of an aws AMI is terminated, we launch a container who are referenced by ``OS type`` and ``OS family``.
2. In that container we execute the ``features`` installation and hooks ``post/pre buildimage``
3. When the build of container is finished, we store it as image in the local registry with an alias who is the ``job id``.
4. Last step, store the alias image in MongoDB to use it as a référence container for future deployment .
5. The container will be destroy

Note: Image retention is based form ami-retention, because a amazon ami always have his container image sources.

**Deployment**

1. Have a buildpack script set in your module
2. If the buildpack is set, so a container will be launch from the image in the local registry who have the alias of the last buildimage job
3. A container profile is create, and set a mount module directory path directly inside it
4. The buildpack script is executed inside the container
5. The container will be destroy

How to enable buildpack in container
************************************

**requirements**

1. Lxd installed from src compilation
2. Lxd daemon run with group lxd
3. Ghost user added to lxd group

**configuration**

1. You just need to select a container in the build infos section
2. Enable debug in config.yml didn't stop the container in buildimage and déployment steps
