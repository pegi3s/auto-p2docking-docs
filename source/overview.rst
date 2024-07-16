What is auto-p2docking?
*******************

**auto-p2docking** is a pipeline maker software, made of a series of bash and python scripts, designed for protein-protein binding inferences. A Docker image is available at `this Docker Hub repository <https://hub.docker.com/r/pegi3s/auto-p2docking>`_.

In addition, it uses Docker images to run any third-party software, thus Docker must be installed (see how to install Docker at <https://pegi3s.github.io/dockerfiles/>`_).

.. _how-to-run:

How to run auto-phylo
*********************

To run **auto-phylo**, you should adapt and run the following command: 

.. code-block:: shell-session

   docker run --rm -v /your/data/dir:/data -v /var/run/docker.sock:/var/run/docker.sock pegi3s/auto-phylo

In this command, you should replace ``/your/data/dir`` to point to the directory that contains the input directory with the files that you want to analyze, as well as the pipeline and config files:

- In the pipeline file you must specify the auto-phylo modules to be invoked as well as the input and output directory names (one per line). 
- In the config file you must declare the path to the working directory as well as the SEDA version to be used, as well as any other parameters that are required by the modules being used.

To help in the creation of such files and to ease pipeline design, a graphical user interface called **auto-phylo-pipeliner** (see :ref:`Pipeliner (GUI)`).

.. Note::
   
   Please, note that in auto-phylo v2, the module parameters are declared in a different way than in `auto-phylo v1 <http://evolution6.i3s.up.pt/static/auto-phylo/v1/docs/>`_. Now, module names are used as parameter prefixes to avoid duplicated parameter names.
