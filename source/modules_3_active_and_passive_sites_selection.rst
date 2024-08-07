Active and passive sites selection
*********

cport_like
-------------

This module allows the identification of active and passive sites in protein sequences. It uses code forked from the repository located at https://github.com/haddocking/cport, and this is the reason behind its name. The code allows to do the automated submission of PDB files to the SCRIBER (http://biomine.cs.vcu.edu/servers/SCRIBER/), SPPIDER (https://sppider.cchmc.org/), PSIVER (https://psiver.mizuguchilab.org/PSIVER/), ISPRED4 (https://ispred4.biocomp.unibo.it/welcome/default/index) and ScanNet (http://bioinfo3d.cs.tau.ac.il/ScanNet/) servers. Being webservers, it is important to configure the number of retries and time between retries to reasonable numbers, depending on how busy the servers are at a given moment. This can be done using the parameters ending in nr (number of retries; ``cport_scribernr=``, ``cport_spiddernr=``, ``cport_psivernr=``, ``cport_ispred4nr=``, ``cport_scannetnr=``) and wi (waiting time; ``cport_scriberwi=``, ``cport_spidderwi=``, ``cport_psiverwi=``, ``cport_ispred4wi=``, ``cport_scannetwi=``). The methods to be used are declared in the ``cport_methods`` parameter separated by whyte spaces around quotation marks (for instance, cport_methods="sppider scannet"). **In contrast to the other modules, the config file where these parameters are to be declared, must be located in the module´s input folder.** The ``cport_exclude`` parameter specifies what to exclude from the analysis. If it is equal to "ligands", the active and passive sites will be calculated only for the receptor, and vice versa. If it is empty, both ligands and receptor will be analyzed. **This parameter is declared in the global config file.** To create the active (1), passive (2) and undetermined (0) categories the following rules are used:

- ISPRED4: values equal or above '0.5' are replaced by '1', less than '0.5' are replaced by '2', and '-' are replaced by '0'.

- SCRIBER: values equal or above '0.5' are replaced by '1', below '0.27' are replaced by '2', and in between '0.27' (including) and '0.5' by '0'. Missing positions are replaced by '0'.

- SPPIDER: 'A' are replaced by '1' and '-' by '0'.

- PSIVER: values equal or above '0.5' are replaced by '1', equal or less than '0.37' are replaced by '2', and in between '0.37' and '0.5' by '0'. Missing positions are replaced by '0'.

- ScanNet: values equal or above '0.5' are replaced by '1', equal or less than '0.35' are replaced by '2', and in between '0,35' and '0.5' by '0'. Missing positions are replaced by '0'.

It should be noted that, if this module is used alone in a single module pipeline, it's necessary to use the copy module to copy all the necessary PDBs to the right place. For example, if the user wishes to
calculate the active and passive sites for a ligand and a receptor, the respective PDBs must be in different input folders in the working_dir. The copy module should then be used to copy the files to PDBs/ligand and PDBs/receptor respectively. The PDB files must have the following UniProtKB_database name structure (for instance, P59665_AF.pdb, P15848_ditasser.pdb).


consensus
--------------------

This module creates a list of active and active sites for each protein according to the information generated by the cport_like module. It takes as input .csv files with the following name structure: UniProtKB_database_server (for instance, P15848_AF_scannet.csv, P15848_AF_psiver.csv). All .csv files must be in a folder named UniProtKB_database (for instance, P15848_AF) inside the module's input folder.
In intermediate files, active sites are labelled as 1, passive sites as 2, and undetermined sites as 0. The rules used for determining whether a given site should be considered as 0, 1, or 2, when looking at the results provided by the different methods being considered, are the following:

- If the number of 0 is greater than the number of 1 and the number of 0 is greater than the number of 2, the site is labelled as 0.
- If the number of 1 is greater than or equal to the number of 0 and the number of 1 is greater than the number of 2, the site is labelled as 1.
- If the number of 2 is greater than or equal to the number of 0 and the number of 2 is greater than the number of 1, the site is labelled as 2.

If the number of active sites is lower than that specified in ``consensus_active_min_number`` then the method that shows the highest number of 1 is chosen to create the list of active
and passive sites. If, as the result of this operation, there are more active sites than the number specified in ``consensus_active_max_number``, the below conditions are applied as well.
If in the consensus there are more active sites than the ones specified in ``consensus_active_max_number``, then a new consensus is calculated based on two methods only (those specified in ``consensus_preferred_1`` and ``consensus_preferred_2`` in two different lines of the config file, for instance: consensus_preferred_1=psiver.csv and consensus_preferred_2=scriber.csv). If this option still produces more active sites than the number specified in ``consensus_active_max_number``, then, if there are two consecutive active sites, the second one is not considered. If this procedure still produces more active sites than the ones specified in ``consensus_active_max_number``, then a random set of active sites is chosen from the consensus produced in the previous step, to fulfil the condition imposed by ``consensus_active_max_number``. It should be noted that if the conditions imposed by ``consensus_active_min_number`` and ``consensus_active_max_number`` are not met based on the original consensus procedure, and if the cport_like and consensus modules are invocated again in the pipeline, the whole procedure will be repeated based on the previous methods plus the new ones. If the condition is, however, met, no action is taken when invoking again the cport_like and consensus modules. If there are fewer active sites than the ones specified in ``consensus_critical_active_number``, then, the ligand being processed is no longer considered when running the remaining modules of the pipeline.
