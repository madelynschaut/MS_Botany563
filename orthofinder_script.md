# orthofinder script from the terminal
```
conda install -c bioconda orthofinder

#return
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /Users/madelynschaut/miniconda3

  added / updated specs:
    - orthofinder
...
Preparing transaction: done
Verifying transaction: done
Executing transaction: done

orthofinder -h

#return
OrthoFinder version 2.5.2 Copyright (C) 2014 David Emms

SIMPLE USAGE:
Run full OrthoFinder analysis on FASTA format proteomes in <dir>
  orthofinder [options] -f <dir>

Add new species in <dir1> to previous run in <dir2> and run new analysis
  orthofinder [options] -f <dir1> -b <dir2>

OPTIONS:
 -t <int>        Number of parallel sequence search threads [Default = 8]
 -a <int>        Number of parallel analysis threads
 -d              Input is DNA sequences
 -M <txt>        Method for gene tree inference. Options 'dendroblast' & 'msa'
                 [Default = dendroblast]
 -S <txt>        Sequence search program [Default = diamond]
                 Options: blast, diamond, diamond_ultra_sens, blast_gz, mmseqs, blast_nucl
 -A <txt>        MSA program, requires '-M msa' [Default = mafft]
                 Options: mafft, muscle
 -T <txt>        Tree inference method, requires '-M msa' [Default = fasttree]
                 Options: fasttree, raxml, raxml-ng, iqtree
 -s <file>       User-specified rooted species tree
 -I <int>        MCL inflation parameter [Default = 1.5]
 -x <file>       Info for outputting results in OrthoXML format
 -p <dir>        Write the temporary pickle files to <dir>
 -1              Only perform one-way sequence search
 -X              Don't add species names to sequence IDs
 -y              Split paralogous clades below root of a HOG into separate HOGs
 -z              Don't trim MSAs (columns>=90% gap, min. alignment length 500)
 -n <txt>        Name to append to the results directory
 -o <txt>        Non-default results directory
 -h              Print this help text

WORKFLOW STOPPING OPTIONS:
 -op             Stop after preparing input files for BLAST
 -og             Stop after inferring orthogroups
 -os             Stop after writing sequence files for orthogroups
                 (requires '-M msa')
 -oa             Stop after inferring alignments for orthogroups
                 (requires '-M msa')
 -ot             Stop after inferring gene trees for orthogroups 

WORKFLOW RESTART COMMANDS:
 -b  <dir>         Start OrthoFinder from pre-computed BLAST results in <dir>
 -fg <dir>         Start OrthoFinder from pre-computed orthogroups in <dir>
 -ft <dir>         Start OrthoFinder from pre-computed gene trees in <dir>

LICENSE:
 Distributed under the GNU General Public License (GPLv3). See License.md

CITATION:
 When publishing work that uses OrthoFinder please cite:
 Emms D.M. & Kelly S. (2019), Genome Biology 20:238

 If you use the species tree in your work then please also cite:
 Emms D.M. & Kelly S. (2017), MBE 34(12): 3267-3278
 Emms D.M. & Kelly S. (2018), bioRxiv https://doi.org/10.1101/267914
```

using a script provided with OrthoFinder to extract just the longest transcript variant per gene and run OrthoFinder on these files
python script is not installed during conda installation-- need to get the python scripts from the github repo:
```
cd ..
cd software
git clone https://github.com/davidemms/OrthoFinder.git

#return
Cloning into 'OrthoFinder'...
remote: Enumerating objects: 8702, done.
remote: Counting objects: 100% (52/52), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 8702 (delta 26), reused 33 (delta 14), pack-reused 8650
Receiving objects: 100% (8702/8702), 31.55 MiB | 17.60 MiB/s, done.
Resolving deltas: 100% (4351/4351), done.
Updating files: 100% (4140/4140), done.
```

running orthofinder
```
orthofinder -f software/

#return
OrthoFinder version 2.5.2 Copyright (C) 2014 David Emms

2021-04-22 14:20:05 : Starting OrthoFinder 2.5.2
8 thread(s) for highly parallel tasks (BLAST searches etc.)
1 thread(s) for OrthoFinder algorithm

Checking required programs are installed
----------------------------------------
Test can run "mcl -h" - ok
Test can run "fastme -i /Users/madelynschaut/Desktop/software/OrthoFinder/Results_Apr22/WorkingDirectory/SimpleTest.phy -o /Users/madelynschaut/Desktop/software/OrthoFinder/Results_Apr22/WorkingDirectory/SimpleTest.tre" - ok

WARNING: Files have been ignored as they don't appear to be FASTA files:
.DS_Store
ADH_grplant_OG0002122.dnd
seqdump.txt
OrthoFinder expects FASTA files to have one of the following extensions: pep, faa, fasta, fa, fas

Dividing up work for BLAST for parallel processing
--------------------------------------------------
2021-04-22 14:20:05 : Creating diamond database 1 of 2
2021-04-22 14:20:05 : Creating diamond database 2 of 2

Running diamond all-versus-all
------------------------------
Using 8 thread(s)
2021-04-22 14:20:05 : This may take some time....
2021-04-22 14:20:10 : Done all-versus-all sequence search

Running OrthoFinder algorithm
-----------------------------
2021-04-22 14:20:10 : Initial processing of each species
2021-04-22 14:20:10 : Initial processing of species 0 complete
2021-04-22 14:20:11 : Initial processing of species 1 complete
2021-04-22 14:20:13 : Connected putative homologues
2021-04-22 14:20:13 : Written final scores for species 0 to graph file
2021-04-22 14:20:13 : Written final scores for species 1 to graph file

WARNING: program called by OrthoFinder produced output to stderr

Command: mcl /Users/madelynschaut/Desktop/software/OrthoFinder/Results_Apr22/WorkingDirectory/OrthoFinder_graph.txt -I 1.5 -o /Users/madelynschaut/Desktop/software/OrthoFinder/Results_Apr22/WorkingDirectory/clusters_OrthoFinder_I1.5.txt -te 1 -V all

stdout
------
b''
stderr
------
b'[mcl] added <194> garbage entries\n'
2021-04-22 14:20:13 : Ran MCL

Writing orthogroups to file
---------------------------
OrthoFinder assigned 228 genes (94.2% of total) to 10 orthogroups. Fifty percent of all genes were in orthogroups with 194 or more genes (G50 was 194) and were contained in the largest 1 orthogroups (O50 was 1). There were 1 orthogroups with all species present and 0 of these consisted entirely of single-copy genes.

2021-04-22 14:20:13 : Done orthogroups

Analysing Orthogroups
=====================

Calculating gene distances
--------------------------
2021-04-22 14:20:16 : Done

Inferring gene and species trees
--------------------------------

Reconciling gene trees and species tree
---------------------------------------
2021-04-22 14:20:19 : Starting Recon and orthologues
2021-04-22 14:20:19 : Starting OF Orthologues
2021-04-22 14:20:19 : Done 0 of 5
2021-04-22 14:20:19 : Done OF Orthologues

Writing results files
=====================
2021-04-22 14:20:19 : Done orthologues

Results:
    /Users/madelynschaut/Desktop/software/OrthoFinder/Results_Apr22/

CITATION:
 When publishing work that uses OrthoFinder please cite:
 Emms D.M. & Kelly S. (2019), Genome Biology 20:238

 If you use the species tree in your work then please also cite:
 Emms D.M. & Kelly S. (2017), MBE 34(12): 3267-3278
 Emms D.M. & Kelly S. (2018), bioRxiv https://doi.org/10.1101/267914
```

a new file was created titled Results_Apr22 in the OrthoFinder folder in my software folder
