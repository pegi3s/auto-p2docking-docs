Divergence estimates
********************

kaks
----

This module is used to calculate nonsynonymous (Ka) and synonymous (Ks) substitution rates by means of various models or model selection and averaging. It accepts as input one FASTA file containing CDS sequences (the first declared nucleotide must always correspond to the first codon position) and returns a tabular formatted file containing nonsynonymous and synonymous substitution rates, as well as other additional information. If no parameters are specified in the config file, it runs with default options (``kaks_model=MA`` and ``kaks_genetic_code=1`` (standard code)). There are many models and genetic codes that can be chosen. Please look at this manual: https://github.com/pegi3s/dockerfiles/blob/master/kakscalculator/2.0/doc/KaKs_Calculator2.0_Manual.pdf. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.