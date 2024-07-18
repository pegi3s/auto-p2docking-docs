PDB retrieval and selection
*********************

getalphafoldpdb
--------

This module allows you to retrieve PDB files from the AF database (https://alphafold.ebi.ac.uk/). It accepts a single text file containing a list of UniprotKB numbers (one per line), located in the input directory, and returns the corresponding files in PDB format from the AF database. The names of the output files are in the following format: UniProtKBnumber_AF.pdb.

getpdb
------------

This module allows retrieving PDB files from the PDB database (https://www.rcsb.org/). It accepts as input a list with UniProtKb numbers, located in the input directory, and returns, if available, the PDB files associated with them. The names of the output files are in the following format: UniProtKBnumber_PDBaccession_PDB.pdb.

getditasserpdb
--------------------------

This module allows you to retrieve PDB files from the HPmod database (https://zhanggroup.org/HPmod/). It accepts a single text file containing a list of UniprotKB numbers (one per line), located in the input directory, and returns the corresponding files in PDB format. The names of the output files are in the following format: UniProtKBnumber_ditasser.pdb.

tm-align-pdb
-------------------

This module allows the automated submission of PDB files obtained from AF, HPmod database, or any other database (file names must not end with the ‘_PDB’ tag) and a PDB file from the PDB database (file names must end with the ‘_PDB’ tag) to the TM-align server (https://zhanggroup.org/TM-align/), in order to select the PDB file with the highest TM score when compared with data from the PDB database (for instance, P15848_AF.pdb and P15848_PDB.pdb, respectively). Only PDB files with the same UniProtKB number will be compared. If no data exists in PDB database for the protein being analyzed, no action is taken.

tm-align-cutoff
------------

This module allows automatic submission of pairs of PDB structures (AF, HPmod, or any other database) to the TM align server (https://zhanggroup.org/TM-align/), to remove PDB files that have very similar structures
(according to the value declared in the variable tm_cutoff_ref). If there is nothing to compare with, no action is taken. The file names are not changed. Only file names starting with the same Uniprot number are compared (for instance, P15848_AF.pdb and P15848_ditasser.pdb). In addition to the tm_cutoff value, the tm_cutoff_order parameter must also be specified in the config file. The tm_cutoff_ref parameter specifies the value of the TM score above which only one of the files being compared will be retained. The file that is retained is declared by the order specificied in the in the tm_cutoff_order parameter (for instance, tm_cutoff_order="AF-ditasser-itasser", which results in the selection of the file with the _AF tag first, if not available, the one with the _ditasser tag, and then, if not available, the one with the _itasser tag).
