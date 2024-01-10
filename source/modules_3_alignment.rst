Alignment
*********

Clustal_Omega
-------------

This module accepts as input a single nucleotide FASTA file, and using the Clustal Omega [2] program, returns as output a single sequence alignment FASTA file. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.

Clustal_Omega_codons
--------------------

This module accepts as input a single CDS FASTA file (sequences must not have stop codons), and returns as output a single sequence alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS transeq feature [3], and an amino acid alignment is obtained using Clustal_Omega [2]. Then, the corresponding nucleotide alignment is obtained using TranslatorX [4]. Therefore, this option is only suitable for FASTA files containing CDS, which is indicated by the "codons" suffix.  Sequences must not have stop codons.

Mafft
-----

This module accepts as input a single nucleotide FASTA file, and using the MAFFT (https://mafft.cbrc.jp/alignment/software/) program, returns as output a single sequence alignment FASTA file. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed in order to remove line breaks from the resulting alignment.

Mafft_codons
------------

This module accepts as input a single CDS FASTA file (sequences must not have stop codons), and returns as output a single sequence alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS transeq feature [3], and an amino acid alignment is obtained using MAFFT (https://mafft.cbrc.jp/alignment/software/). Then, the corresponding nucleotide alignment is obtained using TranslatorX [4]. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed in order to remove line breaks from the resulting alignments. This option is only suitable for FASTA files containing CDS, as indicated by the "codons" suffix.

Probcons
--------

This module accepts as input a single nucleotide FASTA file, and using the PROBCONS (http://probcons.stanford.edu/manual.pdf) program, returns as output a single sequence alignment FASTA file. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.

Probcons_codons
---------------

This module accepts as input a single CDS FASTA file (sequences must not have stop codons), and returns as output a single sequence alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS transeq feature [3], and an amino acid alignment is obtained using PROBCONS [http://probcons.stanford.edu/manual.pdf]. Then, the corresponding nucleotide alignment is obtained using TranslatorX [4]. Therefore, this option is only suitable for FASTA files containing CDS, which is indicated by the "codons" suffix. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.

Probcons_refinement
-------------------

This module accepts as input a single FASTA file containing aligned sequences, and using the PROBCONS (http://probcons.stanford.edu/manual.pdf) program refinement option, returns a refined FASTA file. The number of iterations (``probcons_refin_iterations=``) to be executed in the refinement must be specified in the config file.

T-coffee
--------

This module accepts as input a single FASTA file, and using the T-coffee [10] program, returns as output a single sequence alignment FASTA file.

T-coffee_codons
---------------

As indicated by the "codons" suffix, this module accepts as input a single CDS FASTA file (sequences must not have stop codons), and using the T-coffee [10] program, returns as output a single nucleotide alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS.