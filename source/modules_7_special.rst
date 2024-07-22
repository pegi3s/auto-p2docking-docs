Special
***************

pipeline_drawing
-----------

If "pipeline_drawing" is written in the first line of a pipeline file, then a graphical representation of the pipeline will be produced and the pipeline will not be run. 
This way, it is possible to check if the pipeline has the desired structure. This module is invoked in an automated way when running any pipeline (the resulting file will be saved on the "files_to_keep" folfer).

block
-----------

This is a special command that can be invoked after a regular command and that must be followed by a number (for instance, command input_folder output_folder block 2). It can only be used with the 
following modules: cport_like, consensus, haddock, pydock_ftdock, pisa_server_extract and ccp4_server_extract, allowing these modules to be run for one ligand at a time, and thus allowing the user to obtain 
the docking results as soon as they are obtained for each ligand.
