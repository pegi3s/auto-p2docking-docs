PDB retrieval and selection
*********************

getalphafoldpdb
--------

This module allows you to retrieve PDB files from the AlphaFold database (https://alphafold.ebi.ac.uk/). It accepts a single text file containing a list of UniProtKB identifiers, one per line, located in the input directory, and returns the corresponding structures in PDB format. The names of the output files follow the format ``<protein_id>_AF.pdb``.

This module cannot be used as part of a block and does not require the ligand list.


getpdb
------------

This module allows retrieving PDB files from the PDB database (https://www.rcsb.org/). It accepts as input a list of UniProtKB identifiers located in the input directory and returns, when available, the PDB structures associated with them. The names of the output files follow the format ``<protein_id>_<PDB_accession>_PDB.pdb``.

This module cannot be used as part of a block and does not require the ligand list.


getditasserpdb
--------------------------

This module allows you to retrieve PDB files from the HPmod database (https://zhanggroup.org/HPmod/). It accepts a single text file containing a list of UniProtKB identifiers, one per line, located in the input directory, and returns the corresponding files in PDB format. The names of the output files follow the format ``<protein_id>_ditasser.pdb``.

Structures obtained using this module can also be useful when a PDB structure with a defined chain is required by downstream modules such as ISPRED4, ScanNet or SCRIBER.

This module cannot be used as part of a block and does not require the ligand list.


tm-align-pdb
-------------------

This module allows the automated structural comparison of PDB files obtained from AlphaFold, HPmod or other databases with structures retrieved from the PDB database using TM-align. Candidate structures must not end with the ``_PDB`` tag, whereas reference structures obtained from the PDB database must end with ``_PDB.pdb``. Only structures associated with the same UniProtKB identifier are compared.

For each protein with an available PDB reference structure, the candidate structure with the highest TM-score is selected. If no PDB reference structure is available for a protein, no comparison is performed for that protein. A summary of the calculated TM-scores is also generated.

This module cannot be used as part of a block and does not require the ligand list.


tm-align-cutoff
------------

This module allows automatic structural comparison of PDB structures obtained from AlphaFold, HPmod or other databases using TM-align, in order to remove structures that are considered too similar according to the value defined by ``tm_cutoff_ref``. Only file names starting with the same UniProtKB identifier are compared. If there is nothing to compare, no action is taken and the file names are not changed.

The ``tm_cutoff_ref`` parameter specifies the TM-score above which only one of the structures being compared will be retained. The ``tm_cutoff_order`` parameter specifies the preferred order of the structure sources. For instance, ``tm_cutoff_order="AF-ditasser-itasser"`` gives priority to an ``_AF`` structure, followed by ``_ditasser`` and then ``_itasser`` when available.

This module cannot be used as part of a block and does not require the ligand list.


pdb2fasta
---------

This module allows the conversion of PDB structures into protein sequences in FASTA format using the ``pdb2fasta`` tool from the ``pegi3s/utilities`` Docker image. It accepts a folder containing one or more PDB files and generates a file named ``Fasta_file`` in the output folder, containing the corresponding sequences in FASTA format. Only ``.pdb`` files directly inside the input folder are processed.

For instance, after using the ``copy`` module to place the PDB structures in their respective folders, the following commands can be used in the pipeline file::

   pdb2fasta PDBs/Receptor FASTA/Receptors
   pdb2fasta PDBs/Ligands FASTA/Ligands

These commands generate ``FASTA/Receptors/Fasta_file`` and ``FASTA/Ligands/Fasta_file``, respectively, under the project folder. The resulting FASTA files can be used as input for ``sppider_seq``. A copy of each output is also saved in ``files_to_keep``. The Docker image version can be specified using ``utilities_docker_c_version=`` in the main auto-p2docking config file.

This module cannot be used as part of a block and does not require the ligand or receptor list.
