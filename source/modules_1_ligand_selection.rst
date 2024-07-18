Modules configuration
*********************

It should be noted that in all cases the project directory (``dir=``) and project name (``project=``) must be declared in the main auto-p2docking config file.

Ligand selection
*****

evoppi_querier
-------
This module allows you to retrieve GeneID lists from the EvoPPI databases (http://evoppi.i3s.up.pt). It takes as input a GeneID and returns from EvoPPI the corresponding list(s) of interactors, 
as text files with one GeneID per line. The following parameters must be declared, one per line, in a config file, **which must be in the input folder of the module**:

- evoppi_q_species=
- evoppi_q_geneid=
- evoppi_q_level=
- evoppi_q_intdb=
- evoppi_q_intmod=
- evoppi_q_intpolyq=
- evoppi_q_preddb=
- evoppi_q_predmod=
- evoppi_q_predpolyq=
- evoppi_q_max_int=

where:

- evoppi_q_species indicates the name of the species of interest, for instance "Homo sapiens". The full list of available species can be found in the evoppi_querier_options section.

- evoppi_q_geneid indicates the GeneID for the gene that encodes the protein to be studied.

- evoppi_q_level specifies the interaction level (which is the degree of distance (up to a maximum of three) to retrieve transitive interactions).

- evoppi_q_intdb indicates the name of the interactome databases to be analyzed. The full list of available databases can be found in the evoppi_querier_options section. If more than one database is to be analyzed, their names must be separated by semicolons (for instance, "BioGRID; HIPPIE; Mentha; Mint;Pina2". * means all databases.

- evoppi_q_intmod= indicate the name of the Modifiers interactome
databases to be analysed. The names of the Modifiers interactomes for
the evoppi_q_int.* parameters can be obtained with the following
command: docker run --rm pegi3s/evoppi-querier list_interactomes --
species <species> -dt interactome. In the example provided is: "Homo
sapiens (Modifiers_22)"
- evoppi_q_intpolyq= indicate the name of the PolyQ interactome
databases to be analyzed. The names of the PolyQ interactomes for the
evoppi_q_int.* parameters can be obtained with the following command:
docker run --rm pegi3s/evoppi-querier list_interactomes --species
<species> -dt interactome. In the example provided is: "Homo sapiens
(PolyQ_22)"
- evoppi_q_preddb= indicate the name of the predictomes (predict
interactome) databases to be analyzed. The names of the predictomes
for the evoppi_q_pred.* parameters can be obtained with the following
command: docker run --rm pegi3s/evoppi-querier list_interactomes --
species <Species> -dt predictome. In the example provided is: "Based on
Drosophila melanogaster BioGRID (DIOPT); Based on Drosophila
melanogaster BioGRID (ENSEMBL)"
- evoppi_q_predmod= indicate the name of the Modifiers predictomes
databases to be analyzed. The names of the predictomes for the
evoppi_q_pred.* parameters can be obtained with the following
command: docker run --rm pegi3s/evoppi-querier list_interactomes --
species <Species> -dt predictome. In the example provided is: "*" (select
all available options)
- evoppi_q_predpolyq= indicate the name of the PolyQ predictomes
databases to be analyzed. The names of the predictomes for the
evoppi_q_pred.* parameters can be obtained with the following
command: docker run --rm pegi3s/evoppi-querier list_interactomes --
species <Species> -dt predictome. In the example provided is: "Homo
sapiens Danio rerio (from DIOPT) (PolyQ_models_22)"
- evoppi_q_max_int= Indicate the maximum number of interactions to be
analyzed. In the example provided is: 15
Note 1: all parameters are mandatory, otherwise the program will not run.
evoppi_q_int.* and evoppi_q_pred.* can be empty, but at least one
interactome/predictome name must be specified. If you want to select all available
options, you can use "*" (like evoppi_q_intdb=*).
Note 2: the output folder of EvoPPi accepts up to two output files.


#############This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a
FASTA file for each input file, containing all sequences showing a significant **blastn** 
(https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query (``blastn_query=``) and expect
(``blastn_expect=``) parameters must be specified in two separate lines, in the config file. SEDA-CLI operations
([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to remove line breaks from sequences.

geneid2uniprotkb
-------
This module allows getting the reference UniProtKB number associated with a
given GeneID. It accepts a list of Gene IDs, one per line, and returns a list of UniprotKB numbers
from NCBI gene (https://www.ncbi.nlm.nih.gov/gene), one per line. The input file must have the .gi extension.

intersect
-------
This module allows you to get the intersection of two or more UniProtKB or
GeneID lists. It generates a list of all UniProtKBs or GeneIDs common to all files.

exclude
-------
This module allows you, given two lists of two UniProtKBs/GeneIDs, to get one
list with all UniProtKBs/GeneIDs present in the larger list that are not present in the
smaller list.

copy
-------
This module copies all files from one folder to another. It should be noted that for the pipeline to work,
the PDB files of all ligands must be in a folder named Ligands, and the PDB files of the receptor in a folder 
named Receptor, both under a folder called PDBs, under the project folder (the
variable project is assigned in the config file). Therefore, if this is the intended operation, in the pipeline file, 
it should be declared on two different lines "copy name_of_ligand_input_folder PDBs/Ligands", and "copy name_of_receptor_input_folder PDBs/Receptor". 

human_prot_atlas
-------
This module allows retrieving lists of proteins encoded by genes expressed in a
given tissue. It accepts as input a list with UniProtKb numbers, one per line, and returns
a list of UniProtKb numbers, one per line, of those genes that are expressed in the
specified tissue. In the auto-p2docking configuration file, there are three parameters to be specified (one per line), namely: h_prot_atlas_inc=, h_prot_atlas_mode=, and h_prot_atlas_exc=

- h_prot_atlas_inc: list of tissues to be considered, separated by ;, or * to analyse all available tissues (that is used by default). For instance, h_prot_atlas_inc="Brain_cerebral_cortex; Brain_hippocampal_formation". The list of available tissues are: Brain_cerebral_cortex, Brain_hippocampal_formation,
Brain_amygdala, Brain_basal_ganglia, Brain_thalamus, Brain_hypothalamus,
Brain_midbrain, Brain_cerebellum, Brain_pons, Brain_medulla_oblongata,
Brain_spinal_cord, Brain_white_matter, Choroid_plexus, Salivary_gland, Esophagus,
Tongue, Stomach, Intestine, Pancreas, Kidney, Urinary_bladder, Breast, Vagina, Cervix,
Endometrium, Fallopian_tube, Ovary, Placenta, Skin, Adipose_tissue,
Seminal_vesicles, Prostate, Epididymis, Testis, Gallbladder, Liver, Lymphoid_tissue,
Bone_marrow, Lung, Pituitary_gland, Thyroid_gland, Parathyroid_gland,
Adrenal_gland, Smooth_muscle, Heart, Retina.

- h_prot_atlas_mode: you can select all proteins by writing union or only those
that are present in all selected tissues if you write intersection . If you do
not provide information in this field, union is used by default.

- h_prot_atlas_exc: If h_prot_atlas_inc=* has been declared, you can exclude specific tissue(s) by indicating their name(s), separated by ;.
