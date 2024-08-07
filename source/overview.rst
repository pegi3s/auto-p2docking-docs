What is auto-p2docking v1?
*******************

**auto-p2docking** is a pipeline maker software, made of a series of bash and python scripts, designed for protein-protein binding inferences. A Docker image is available at `this Docker Hub repository <https://hub.docker.com/r/pegi3s/auto-p2docking>`_.

It uses Docker images to run third-party software, and thus, Docker must be installed (see how to install Docker at https://pegi3s.github.io/dockerfiles/). Please note that, due to copyright issues, some Docker images must be build according to the instructions given in the pegi3S Bioinformatics Docker Images Project (https://pegi3s.github.io/dockerfiles/) for ``haddock24-builder``, ``hdock-builder``, and ``pydock3-builder``. If such Docker images are not build according to the provided instructions, the corresponding modules that use them will not run (haddock, hdock, and pydock_ftdock, respectively).

**This manual will be updated when new modules, protocols, or features are added to auto-p2docking, as long as the changes are backwards-compatible. Therefore, it may describe modules, protocols or features that are not present in earlier versions.**

.. _how-to-run:

How to run auto-phylo
*********************

To run **auto-phylo**, you should adapt and run the following command: 

.. code-block:: shell-session

   docker run --rm -v /your/data/dir:/data -v /var/run/docker.sock:/var/run/docker.sock pegi3s/auto-p2docking

In this command, you should replace ``/your/data/dir`` to point to the directory that contains the input directory with the files that you want to analyze, as well as the pipeline and config files:

- In the pipeline file you must specify the auto-p2docking modules to be invoked as well as the input and output directory names (one per line). 
- In the config file you must declare the path to the working directory (dir=), the project name (project=), and any other parameters that are required by the modules being used (see modules description).

.. Note::
   
   Please, note that module names (or acronyms) are used as parameter prefixes to avoid duplicated parameter names.
