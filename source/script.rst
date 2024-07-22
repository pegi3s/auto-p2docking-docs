auto-phylo script basic structure
*********************************

This section presents the basic structure of an **auto-p2docking** script.

The structure of a basic auto-p2docking script is relatively simple as the figure
below shows, and thus, even a researcher with very basic knowledge on bash scripting should be able to write a simple
module, especially if a Docker image that implements the desired software is already available. Assuming 
that such module is named my_module and that it is located in the working directory (``/your/data/dir``), it can be
copied into the Docker image, and then be invoked as any other auto-p2docking module, with the following command:

.. code-block:: docker

    docker run --rm \
        -v /your/data/dir:/data \
        -v /var/run/docker.sock:/var/run/docker.sock \
            pegi3s/auto-p2docking bash -c "cp /data/my_module /opt && /opt/main"

The following figure shows the basic structure of an auto-phylo script.

.. figure:: images/script.png
   :align: center
   :width: 600px

Where:

1. Command lines required by all auto-p2docking scripts.
2. Lines required for version control.
3. Lines required for changing the default Docker images versions.
4. Informative message.
5. Creates the directory where the result of the operation listed below will be saved. Do not forget to declare the ``$prefix`` variable.
6. Instructions regarding the module´s function.
7. The input directory of the first operation must be ``/data/$input_dir`` (the variable ``$input_dir`` captures the name of the input directory declared in the pipeline file).
8. The name of the output directory of the first operation, that should be, in case the pipeline is not branched, the input directory of the second operation.
9. The parameters of the specified operation. Variables defined in the config file can be used, by invoking ``$variable_name``.
10. Instruction to hide the output usually shown in the console.
11. Creates the output directory specified in the pipeline file.
12. Copies the relevant output to the output directory specified in the pipeline file (in this case by invoking the wildcard \*, we are assuming that all files are relevant).
