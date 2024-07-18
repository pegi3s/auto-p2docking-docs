Version customization
*******************

In **auto-p2docking** the module versions and the versions of the Docker images used by the modules are strictly controlled, and are printed in a file called "versions.csv" whenever a given module is used. 
Nevertheless, it is possible to change the version of the Docker images used by each module. To do this, simply add the appropriate parameter from the list below to the auto-p2docking config file with
the desired version. It should be noted that the Docker image to be used must belong to the pegi3s/Bioinformatics Docker Images Project (https://pegi3s.github.io/dockerfiles/).

- cport_like_docker_c_version=
- evoppi_docker_c_version=
- geneid2uniprotkb_docker_c_version=
- getalphafoldpdb_docker_c_version=
- getditasserpdb_docker_c_version=
- getpdb_docker_c_version=
- haddock_docker_version=
- hdock_docker_version=
- highlightregions_docker_version=
- hprotatlas_docker_version=
- pisaccp4_docker_version=
- pisaserver_docker_version=
- pisaxmlextract_docker_version=
- pydock_program_version=
- tmaligncutoff_docker_version=
- tmalignpdb_docker_version=

It uses Docker images to run third-party software, and thus, Docker must be installed (see how to install Docker at https://pegi3s.github.io/dockerfiles/).

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
