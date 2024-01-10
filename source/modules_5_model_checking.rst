Model checking
**************

JModel_test
-----------

This module  accepts as input a nucleotide alignment in FASTA format, and using the JModel [7] test program, produces as an output a report, that can be used to check whether the GTR+I+G model used by the Fasttree [5] and MrBayes [8] modules is appropriate. Before running JModel test, sequence headers are renamed (using SEDA-CLI operations; [1]; https://hub.docker.com/r/pegi3s/seda/), since this program does not allow special characters in sequence header names besides underscores.
