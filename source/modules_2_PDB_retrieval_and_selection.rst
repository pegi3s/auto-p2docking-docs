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

This module allows the automated submission of PDB files obtained from AF, HPmod database, or any other database (file names must not end with the ‘_PDB’ tag) and a PDB file from the PDB database (file names must end with the ‘_PDB’ tag) to the TM-align server (https://zhanggroup.org/TM-align/), in order to select the PDB file with the highest TM score when compared with data from the PDB database. Only PDB files with the same UniProtKB number will be compared. If no data exists in PDB database for the protein being analyzed, no action is taken.

tm-align-cutoff
------------

This module allows automatic submission of pairs of PDB structures (AF, HPmod, or any other database) to the TM align server (https://zhanggroup.org/TM-align/), to remove PDB files that have very similar structures
(according to the value declared in the variable tm_cutoff_ref). If there is nothing to compare with, no action is taken. The file names are not changed. Only file names starting with the same Uniprot number are compared.
Example:
tm_cutoff_ref=0.45
tm_cutoff_order="AF-ditasser-itasser"
Parameter description:
- tm_cutoff_ref= Specifies the minimum value of the TM score. If the TMscore
value is above that declared, then the file that is retained is the one
first matching one of the tags declared in the variable tm_cutoff_order=. If
the TM-score is below the one specified in the tm_cutoff_ref parameter,
both PDB files will be kept. In the example given is 0.45
- tm_cutoff_order= Specifies the order of the files to be kept. In the example
provided is "AF-ditasser-itasser" which would select the AF .pdb if the TMscore
is above the tm_cutoff_ref parameter.
