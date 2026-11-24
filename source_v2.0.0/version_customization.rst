Version customization
*********************

In **auto-p2docking**, the module versions and the versions of the Docker images used by the modules are strictly controlled and are recorded in a file named ``versions.csv`` under the ``files_to_keep`` folder whenever a module is used.

Nevertheless, it is possible to change the version of the Docker images used by several modules. To do this, add the corresponding parameter from the list below to the main auto-p2docking config file and specify the desired version.

It should be noted that the Docker image to be used must belong to the pegi3s Bioinformatics Docker Images Project (https://pegi3s.github.io/dockerfiles/).

- ``evoppi_docker_c_version=``
- ``geneid2uniprotkb_docker_c_version=``
- ``getalphafoldpdb_docker_c_version=``
- ``getditasserpdb_docker_c_version=``
- ``getpdb_docker_c_version=``
- ``haddock_docker_c_version=``
- ``hdock_docker_c_version=``
- ``highlightregions_docker_c_version=``
- ``hprotatlas_docker_c_version=``
- ``pesto_docker_c_version=``
- ``pisaccp4_docker_c_version=``
- ``pisaserver_docker_c_version=``
- ``pisaxmlextract_docker_c_version=``
- ``prodigy_docker_c_version=``
- ``pydock_docker_c_version=``
- ``pymol_docker_c_version=``
- ``scriber_docker_c_version=``
- ``sppider_seq_docker_c_version=``
- ``tmaligncutoff_docker_c_version=``
- ``tmalignpdb_docker_c_version=``
- ``tmtoolsalignpdb_docker_c_version=``
- ``utilities_docker_c_version=``