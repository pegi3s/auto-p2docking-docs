Modules configuration
*********************

It should be noted that in all cases the project directory (``dir=``) must be declared. Moreover, if SEDA-CLI operations are used, the SEDA version (``SEDA=``) should be declared as well.

BLAST
*****

blastn
-------
This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a
FASTA file for each input file, containing all sequences showing a significant **blastn** 
(https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query (``blastn_query=``) and expect
(``blastn_expect=``) parameters must be specified in two separate lines, in the config file. SEDA-CLI operations
([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to remove line breaks from sequences.

tblastn
-------
This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a
FASTA file for each input file, containing all sequences showing a significant **tblastn** 
(https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query (``tblastn_query=``) and expect
(``tblastn_expect=``) parameters must be specified in two separate lines, in the config file. SEDA-CLI operations 
([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to remove line breaks from sequences.

tblastx
-------
This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a
FASTA file for each input file, containing all sequences showing a significant **tblastx**
(https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query (``tblastx_query=``) and expect
(``tblastx_expect=``) parameters must be specified in two separate lines, in the config file. SEDA-CLI operations 
([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to remove line breaks from sequences.
