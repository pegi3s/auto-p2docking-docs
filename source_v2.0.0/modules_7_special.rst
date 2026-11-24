Special
***************

pipeline_drawing
-----------

If ``pipeline_drawing`` is written in the first line of a pipeline file, a graphical representation of the pipeline will be produced and the pipeline will not be run. 
This way, it is possible to check if the pipeline has the desired structure. 
This module is also invoked automatically when running any pipeline, and the resulting file is saved in the ``files_to_keep`` folder.


block
-----------

This is a special option that can be added after a regular command and must be followed by the number of consecutive commands that belong to the block (for instance, ``command input_folder output_folder block 2``). 
A block groups consecutive modules that support block execution and runs the complete sequence for one ligand before proceeding to the next ligand, allowing the user to obtain results for each ligand without waiting for all ligands to finish each individual module first.

Only modules configured with block support can be included in a block. These currently include ``hdock``, ``pydock_ftdock``, ``haddock``, ``consensus``, ``ispip``, ``ispred4``, ``pesto``, ``pipenn``, ``scriber``, ``prodigy`` and ``scannet``.