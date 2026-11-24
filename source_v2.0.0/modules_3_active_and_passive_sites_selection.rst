Active and passive sites selection
**********************************

PeSTo
-------------

This module allows the prediction of protein-protein interaction sites using PeSTo. 
It takes PDB files as input and generates a .csv file containing the predicted interface residues in the format required by the consensus module. 
To create the active (1), passive (2) and undetermined (0) categories in auto-p2docking, B-factor values equal or above '0.5' are replaced by '1', values equal or below '0.25' are replaced by '2', and values between '0.25' and '0.5' are replaced by '0'. 
For each input structure, a file named according to the protein identifier and the prediction method is generated (for instance, ``<protein_id>.pesto.csv``).

If running this module alone, the ``copy`` command must first be used to place the PDB files in ``PDBs/Ligands`` or ``PDBs/Receptor``, according to the structures being analyzed.

This module can be used as part of a block and requires the corresponding ligand or receptor list. 

If the input PDB file does not contain chain information, a structure generated with ``getditasserpdb`` can be used before this module to obtain a PDB file with a defined chain.


ISPRED4
-------------

This module allows the prediction of protein-protein interaction sites using ISPRED4. 
It takes a PDB file as input and generates a .csv file containing the prediction for each amino acid residue. 
The chain to be analyzed must be specified in the main auto-p2docking config file using the ``ispred4_chain=`` parameter (for instance, ``ispred4_chain="A"``). 
To create the active (1), passive (2) and undetermined (0) categories in auto-p2docking, probabilities equal or above '0.50' are replaced by '1', probabilities equal or below '0.25' are replaced by '2', values between '0.25' and '0.50' are replaced by '0', and missing probabilities or '-' are replaced by '0'. 
For each input structure, a file named according to the protein identifier and the prediction method is generated (for instance, ``<protein_id>.ispred4.csv``).

If running this module alone, the ``copy`` command must first be used to place the PDB files in ``PDBs/Ligands`` or ``PDBs/Receptor``, according to the structures being analyzed.

This module can be used as part of a block and requires the corresponding ligand or receptor list. 

If the input PDB file does not contain chain information, a structure generated with ``getditasserpdb`` can be used before this module to obtain a PDB file with a defined chain.


ScanNet
-------------

This module allows the prediction of protein-protein interaction sites using ScanNet. 
It takes a PDB file as input and generates a .csv file containing the prediction for each amino acid residue. 
The chain to be analyzed must be specified in the main auto-p2docking config file using the ``scannet_chain=`` parameter (for instance, ``scannet_chain="A"``). 
To create the active (1), passive (2) and undetermined (0) categories in auto-p2docking, values equal or above '0.5' are replaced by '1', values equal or below '0.35' are replaced by '2', and values between '0.35' and '0.5' are replaced by '0'. Missing positions are replaced by '0'. 
For each input structure, a file named according to the protein identifier and the prediction method is generated (for instance, ``<protein_id>.scannet.csv``).

If running this module alone, the ``copy`` command must first be used to place the PDB files in ``PDBs/Ligands`` or ``PDBs/Receptor``, according to the structures being analyzed.

This module can be used as part of a block and requires the corresponding ligand or receptor list. 

If the input PDB file does not contain chain information, a structure generated with ``getditasserpdb`` can be used before this module to obtain a PDB file with a defined chain.


SCRIBER
-------------
.. Note::

   The SCRIBER module requires permission to use the SCRIBER server. The user must have access to the service before running this module.

This module allows the prediction of protein-protein interaction sites using SCRIBER. 
It takes a PDB file as input and generates a .csv file containing the predicted interface residues. 
The chain to be analyzed must be specified in the main auto-p2docking config file using the ``scriber_chain=`` parameter (for instance, ``scriber_chain="A"``). 
To create the active (1) and passive (2) categories in auto-p2docking, residues returned by SCRIBER as active are assigned code '1', while residues returned as passive are assigned code '2'. 
For each input structure, a file named according to the protein identifier and the prediction method is generated (for instance, ``<protein_id>.scriber.csv``).

If running this module alone, the ``copy`` command must first be used to place the PDB files in ``PDBs/Ligands`` or ``PDBs/Receptor``, according to the structures being analyzed.

This module can be used as part of a block and requires the corresponding ligand or receptor list. 

If the input PDB file does not contain chain information, a structure generated with ``getditasserpdb`` can be used before this module to obtain a PDB file with a defined chain.


PIPENN
-------------

This module allows the prediction of protein-protein interaction sites using PIPENN. 
It takes PDB files as input and generates a .csv file containing the predicted interface residues in the format required by the consensus module. 
To create the active (1), passive (2) and undetermined (0) categories in auto-p2docking, prediction scores equal or above '0.5' are replaced by '1', scores equal or below '0.25' are replaced by '2', and values between '0.25' and '0.5' are replaced by '0'. 
For each input structure, a file named according to the protein identifier and the prediction method is generated (for instance, ``<protein_id>.pipenn.csv``).

If running this module alone, the ``copy`` command must first be used to place the PDB files in ``PDBs/Ligands`` or ``PDBs/Receptor``, according to the structures being analyzed.

This module can be used as part of a block and requires the corresponding ligand or receptor list.

If the input PDB file does not contain chain information, a structure generated with ``getditasserpdb`` can be used before this module to obtain a PDB file with a defined chain.


SPPIDER-seq
-------------

This module allows the prediction of protein-protein interaction sites using SPPIDER-seq. Unlike the other prediction modules, it takes protein sequences in FASTA format as input, including files containing multiple sequences (multi-FASTA). The query sequence and the interaction partners must be specified in a file named ``config``, placed in the module input folder. The following parameters are required:

- ``query``: the FASTA file containing the query sequence(s).
- ``partners``: one or more FASTA files containing the interaction partner sequence(s), separated by spaces.

For instance, after generating the FASTA files using ``pdb2fasta``, the input folder's ``config`` file may contain::

   [Inputs]
   query = receptors_list
   partners = ligands_list

The ``receptors_list`` and ``ligands_list`` names refer to the files ``FASTA/Receptors/Fasta_file`` and ``FASTA/Ligands/Fasta_file`` in the project folder, respectively, and not to the PDB list files. The corresponding ``PDBs/receptors_list.txt`` and ``PDBs/ligands_list.txt`` must also have been created using ``copy``. Alternatively, ``query`` and ``partners`` can specify the paths to existing FASTA files. The ``[Inputs]`` heading is optional.

For a pipeline that uses these aliases, the following commands can be used::

   copy receptor_inputs PDBs/Receptor
   copy ligand_inputs PDBs/Ligands
   pdb2fasta PDBs/Receptor FASTA/Receptors
   pdb2fasta PDBs/Ligands FASTA/Ligands
   sppider_seq sppider_input SPPIDER_results

The ``sppider_seq_scrambles`` parameter can be declared in the main auto-p2docking config file to specify the number of sequence scrambles to perform (``0`` by default). The Docker image version can be specified using ``sppider_seq_docker_c_version=``. For compatibility with older protocols, ``sppider_seq_query`` and ``sppider_seq_partners`` can still be declared in the main config file when no module-specific ``config`` file is present.

For each partner FASTA file, SPPIDER-seq creates a ``prediction_01``, ``prediction_02``, etc. folder containing the original prediction results. A ``sppider_seq_runs.csv`` file is also generated to summarize the analyzed query-partner pairs and their output locations. Unlike the other prediction modules, the current implementation does not automatically convert its results to the active (1), passive (2) and undetermined (0) categories or to the file format required by ``consensus``.

This module cannot be used as part of a block and does not require the ligand or receptor list for per-protein processing.


consensus
--------------------

This module creates a consensus list of active and passive sites for each protein using the results generated by the different protein-protein interaction site prediction modules. 
The input must contain one folder for each protein. Inside each protein folder, prediction files must follow the naming structure ``<protein_id>.<method>.csv`` (for instance, ``<protein_id>.pesto.csv`` or ``<protein_id>.scannet.csv``). 
In the prediction files, active sites are labelled as 1, passive sites as 2, and undetermined sites as 0. Residues that are not present in one of the prediction files are considered undetermined (0) for that method.

For each residue, the consensus is determined according to the following rules:

- If 0 is the most frequent value, the residue is labelled as 0.
- If 1 is at least as frequent as 0 and more frequent than 2, the residue is labelled as 1.
- If 2 is at least as frequent as 0 and more frequent than 1, the residue is labelled as 2.
- If none of these conditions is met, the residue is labelled as 0.

The minimum and maximum acceptable numbers of active sites are defined by ``consensus_active_min_number`` and ``consensus_active_max_number`` in the main auto-p2docking config file. 
If the original consensus does not fall within this range, alternative selection procedures are applied. 
These may use the prediction method with the highest number of active sites or a new consensus based on the preferred methods defined by ``consensus_preferred_1`` and ``consensus_preferred_2``. 
Additional filtering may then be applied to reduce the number of active sites when necessary. 
The ``consensus_critical_active_number`` parameter defines the minimum critical number of active sites. If this condition is not met during the alternative procedures, the protein is marked so that it will not be processed by subsequent modules. 
The final output contains the selected consensus result and the files ``<protein_id>_active.sites`` and ``<protein_id>_passive.sites``.

This module can be used as part of a block and requires the corresponding ligand or receptor list.