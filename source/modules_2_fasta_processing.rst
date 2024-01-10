FASTA file processing
*********************

add_refs
--------
This module accepts as input a single FASTA file containing one or multiple reference sequences to be added to a single file that is the result of the merging of all FASTA files located in the input folder. It returns as output a single FASTA file, named "refseq_added”, with the content of all files located in the input folder and the reference sequences. The name of the file containing the reference sequences must be specified in the config file (``add_refs_reference=``). SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed in order to merge the FASTA files and remove line breaks from sequences.

add_taxonomy
------------

This module accepts as input one or multiple FASTA files downloaded from the NCBI assembly database, and adds taxonomy information to the headers of FASTA files, using the SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/), as long as the corresponding GCF or GCA accession number is part of the file name. This is achieved by querying NCBI, and thus, there is always the possibility that the internet connection will fail. In that case, the affected FASTA will be moved to the folder "2-Files_that_failed" under the corresponding block and command directory. It is advisable to check this folder. It returns as output as many FASTA files as the ones given as input. The parameter ``add_tax_taxonomy_header=`` must be declared in the config file (for instance, ``add_tax_taxonomy_header="Class Family"``).

CGF_and_CGA_CDS_processing
--------------------------

This module accepts as input one or multiple CDS FASTA files downloaded from the NCBI assembly database, and using SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/), implements the following operations:  1) sequence headers are reformatted in order to keep only the scaffold and protein accession numbers; 2) Sequences showing ambiguous nucleotides are removed; 3) only sequences showing a valid start codon, that do not have in frame stop codons, and that are multiple of three are kept; 4) stop codons are removed; 5) sequences showing a size variation (in percentage) relative to the reference sequence greater than the specified value are not kept; 6) only sequences showing the specified pattern are kept; 7) isoforms are removed. The following parameters must be specified in the config file: ``cgf_cga_start_codon`` (a list of valid start codons with one space between them), ``cgf_cga_max_size_difference`` (the maximum difference (in percentage) allowed, relative to the sequence given in the reference file, to consider a given sequence as being of interest), ``cgf_cga_reference_file`` (the name of the reference FASTA file containing a single nucleotide), ``cgf_cga_pattern`` (regular expression), ``cgf_cga_codon_table`` (the codon table that should be used for translation), ``cgf_cga_isoform_min_word_length`` (the minimum identical word size for two sequences to be inferred as isoforms), and ``cgf_cga_isoform_ref_size`` (the reference size that is used to decide which one of two isoforms should be kept. The one with the closest size will be kept). It should be noted, that if the size variation (in percentage) relative to the reference sequence is a large number (for instance, 100000), the specified pattern is ".”, or the isoform minimum word length is greater than the sequence sizes, the corresponding operations will be effectively ignored. It returns as output as many files as the ones given as input. When processing a large number of files, in order to avoid out of memory errors, it is advisable to use the split option (see below).

check_contamination
-------------------

This module accepts as input one or multiple FASTA files downloaded from the NCBI assembly database, and adds the taxonomy specified in the config file (``check_cont_taxonomy=``) to the name of the file as a suffix, using the SEDA-cli ([1]; https://hub.docker.com/r/pegi3s/seda/) operations. The value of this suffix is then compared with the value declared for category in the config file (``check_cont_category=``). If the there is a discrepancy, then the file is treated as being a putative contaminant. This is achieved by querying NCBI, and thus, there is always the possibility that the internet connection will fail. In that case, the affected FASTA will be moved to the folder "4-Suspicious_Files" under the corresponding block and command directory. It is advisable to always check this folder. If there are no contaminations, it returns as many FASTA files as the ones given as input.

disambiguate
------------

This module takes as input one or multiple FASTA files. Using SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/) operations, identical sequence headers are disambiguated using an incremental suffix. It returns as output as many files as the ones given as input.

merge
-----

This module merges all FASTA files in a given folder into a single one, and removes redundant identical sequences or sub-sequences, using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/) operations, thus allowing the user to specify modules that accept a single FASTA file in the following step.

prefix
------

This module accepts as input one or more FASTA files. It adds a prefix to the sequence headers, using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/)  operations. Some programs (for instance, Blast (https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) or MrBayes [8]) have a size limit for sequence headers, and thus, in the auto-phylo modules that use these programs, the headers are truncated to meet such requirements. Nevertheless, in the truncated header versions, two header names may become identical. In order to avoid such possibility, a prefix may be added to sequence names. It returns as many FASTA files as the ones given as input.

prefix_out
----------

This module accepts as input one or more FASTA files. Using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/)  operations, it removes the prefixes that are added by the prefix module, and returns as many FASTA files as the ones given as input.

remove_stops
------------

This module accepts as input one or more FASTA files. Using SEDA-CLI using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/) operations, it removes stop codons from sequences, and returns as many FASTA files as the ones given as input. The alignment of CDS sequences using either the Clustal_Omega_codons or the T-coffee_codons modules, requires that CDS sequences do not have stop codons.