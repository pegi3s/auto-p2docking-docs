Version customization
*******************

In **auto-p2docking** the module versions and the versions of the Docker images used by the modules are strictly controlled, and are printed in a file called "versions.csv" (under the files_to_keep folder) whenever a given module is used. Nevertheless, it is possible to change the version of the Docker images used by each module. To do this, simply add the appropriate parameter from the list below to the auto-p2docking config file with the desired version. It should be noted that the Docker image to be used must belong to the pegi3s/Bioinformatics Docker Images Project (https://pegi3s.github.io/dockerfiles/).

- ``cport_like_docker_c_version=``
- ``evoppi_docker_c_version=``
- ``geneid2uniprotkb_docker_c_version=``
- ``getalphafoldpdb_docker_c_version=``
- ``getditasserpdb_docker_c_version=``
- ``getpdb_docker_c_version=``
- ``haddock_docker_c_version=``
- ``hdock_docker_c_version=``
- ``highlightregions_docker_c_version=``
- ``hprotatlas_docker_c_version=``
- ``pisaccp4_docker_c_version=``
- ``pisaserver_docker_c_version=``
- ``pisaxmlextract_docker_c_version=``
- ``pydock_program_c_version=``
- ``tmaligncutoff_docker_c_version=``
- ``tmalignpdb_docker_c_version=``
