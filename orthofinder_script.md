# orthofinder script from the terminal

used bioconda to install orthofinder:
```
conda install -c bioconda orthofinder
```

the following was returned:
```
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
```

then, to confirm if orthofider was correctly installed, i ran:
```
orthofinder -h
```

the following was returned:
```
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

it appears that orthofinder was successfully installed!

used a script provided with OrthoFinder to extract just the longest transcript variant per gene and run OrthoFinder on these files
python script is not installed during conda installation-- need to get the python scripts from the github repo:
```
cd ..
cd software
git clone https://github.com/davidemms/OrthoFinder.git
```

the following was returned:
```
Cloning into 'OrthoFinder'...
remote: Enumerating objects: 8702, done.
remote: Counting objects: 100% (52/52), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 8702 (delta 26), reused 33 (delta 14), pack-reused 8650
Receiving objects: 100% (8702/8702), 31.55 MiB | 17.60 MiB/s, done.
Resolving deltas: 100% (4351/4351), done.
Updating files: 100% (4140/4140), done.
```

ran orthofinder
```
orthofinder -f species_files/
```

the following was returned:
```
OrthoFinder version 2.5.2 Copyright (C) 2014 David Emms

2021-04-30 18:19:56 : Starting OrthoFinder 2.5.2
8 thread(s) for highly parallel tasks (BLAST searches etc.)
1 thread(s) for OrthoFinder algorithm

Checking required programs are installed
----------------------------------------
Test can run "mcl -h" - ok
Test can run "fastme -i /Users/madelynschaut/Desktop/Botany563_FinalProject/software/species_files/OrthoFinder/Results_Apr30/WorkingDirectory/SimpleTest.phy -o /Users/madelynschaut/Desktop/Botany563_FinalProject/software/species_files/OrthoFinder/Results_Apr30/WorkingDirectory/SimpleTest.tre" - ok

WARNING: Files have been ignored as they don't appear to be FASTA files:
.DS_Store
OrthoFinder expects FASTA files to have one of the following extensions: fasta, fas, pep, faa, fa

Dividing up work for BLAST for parallel processing
--------------------------------------------------
2021-04-30 18:19:56 : Creating diamond database 1 of 20
2021-04-30 18:19:56 : Creating diamond database 2 of 20
2021-04-30 18:19:56 : Creating diamond database 3 of 20
2021-04-30 18:19:56 : Creating diamond database 4 of 20
2021-04-30 18:19:56 : Creating diamond database 5 of 20
2021-04-30 18:19:56 : Creating diamond database 6 of 20
2021-04-30 18:19:56 : Creating diamond database 7 of 20
2021-04-30 18:19:56 : Creating diamond database 8 of 20
2021-04-30 18:19:56 : Creating diamond database 9 of 20
2021-04-30 18:19:56 : Creating diamond database 10 of 20
2021-04-30 18:19:56 : Creating diamond database 11 of 20
2021-04-30 18:19:56 : Creating diamond database 12 of 20
2021-04-30 18:19:56 : Creating diamond database 13 of 20
2021-04-30 18:19:56 : Creating diamond database 14 of 20
2021-04-30 18:19:56 : Creating diamond database 15 of 20
2021-04-30 18:19:56 : Creating diamond database 16 of 20
2021-04-30 18:19:56 : Creating diamond database 17 of 20
2021-04-30 18:19:56 : Creating diamond database 18 of 20
2021-04-30 18:19:56 : Creating diamond database 19 of 20
2021-04-30 18:19:56 : Creating diamond database 20 of 20

Running diamond all-versus-all
------------------------------
Using 8 thread(s)
2021-04-30 18:19:56 : This may take some time....
2021-04-30 18:19:57 : Done 0 of 400
2021-04-30 18:19:59 : Done 100 of 400
2021-04-30 18:20:01 : Done 200 of 400
2021-04-30 18:20:04 : Done 300 of 400
2021-04-30 18:20:07 : Done all-versus-all sequence search

Running OrthoFinder algorithm
-----------------------------
2021-04-30 18:20:07 : Initial processing of each species
2021-04-30 18:20:07 : Initial processing of species 0 complete
WARNING: Too few hits between species 1 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 1 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 1 complete
2021-04-30 18:20:08 : Initial processing of species 2 complete
WARNING: Too few hits between species 3 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 3 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 3 complete
2021-04-30 18:20:08 : Initial processing of species 4 complete
2021-04-30 18:20:08 : Initial processing of species 5 complete
WARNING: Too few hits between species 6 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 6 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 6 complete
WARNING: Too few hits between species 7 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 7 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 7 complete
2021-04-30 18:20:08 : Initial processing of species 8 complete
2021-04-30 18:20:08 : Initial processing of species 9 complete
WARNING: Too few hits between species 10 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 10 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 10 complete
WARNING: Too few hits between species 11 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 11 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 11 complete
WARNING: Too few hits between species 12 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 12 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 12 complete
WARNING: Too few hits between species 13 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 13 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 13 complete
WARNING: Too few hits between species 14 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 14 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 14 complete
WARNING: Too few hits between species 15 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 15 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 15 complete
2021-04-30 18:20:08 : Initial processing of species 16 complete
WARNING: Too few hits between species 17 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 17 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:08 : Initial processing of species 17 complete
2021-04-30 18:20:09 : Initial processing of species 18 complete
WARNING: Too few hits between species 19 and species 1 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 3 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 6 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 7 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 10 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 11 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 12 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 13 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 14 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 15 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 17 to normalise the scores, these hits will be ignored
WARNING: Too few hits between species 19 and species 19 to normalise the scores, these hits will be ignored
2021-04-30 18:20:09 : Initial processing of species 19 complete
2021-04-30 18:20:12 : Connected putative homologues
2021-04-30 18:20:12 : Written final scores for species 0 to graph file
2021-04-30 18:20:12 : Written final scores for species 1 to graph file
2021-04-30 18:20:12 : Written final scores for species 2 to graph file
2021-04-30 18:20:12 : Written final scores for species 3 to graph file
2021-04-30 18:20:12 : Written final scores for species 4 to graph file
2021-04-30 18:20:12 : Written final scores for species 5 to graph file
2021-04-30 18:20:12 : Written final scores for species 6 to graph file
2021-04-30 18:20:12 : Written final scores for species 7 to graph file
2021-04-30 18:20:12 : Written final scores for species 8 to graph file
2021-04-30 18:20:12 : Written final scores for species 9 to graph file
2021-04-30 18:20:12 : Written final scores for species 10 to graph file
2021-04-30 18:20:13 : Written final scores for species 11 to graph file
2021-04-30 18:20:13 : Written final scores for species 12 to graph file
2021-04-30 18:20:13 : Written final scores for species 13 to graph file
2021-04-30 18:20:13 : Written final scores for species 14 to graph file
2021-04-30 18:20:13 : Written final scores for species 15 to graph file
2021-04-30 18:20:13 : Written final scores for species 16 to graph file
2021-04-30 18:20:13 : Written final scores for species 17 to graph file
2021-04-30 18:20:13 : Written final scores for species 18 to graph file
2021-04-30 18:20:13 : Written final scores for species 19 to graph file

WARNING: program called by OrthoFinder produced output to stderr

Command: mcl /Users/madelynschaut/Desktop/Botany563_FinalProject/software/species_files/OrthoFinder/Results_Apr30/WorkingDirectory/OrthoFinder_graph.txt -I 1.5 -o /Users/madelynschaut/Desktop/Botany563_FinalProject/software/species_files/OrthoFinder/Results_Apr30/WorkingDirectory/clusters_OrthoFinder_I1.5.txt -te 1 -V all

stdout
------
b''
stderr
------
b'[mcl] added <4> garbage entries\n'
2021-04-30 18:20:13 : Ran MCL

Writing orthogroups to file
---------------------------
OrthoFinder assigned 36 genes (100.0% of total) to 2 orthogroups. Fifty percent of all genes were in orthogroups with 32 or more genes (G50 was 32) and were contained in the largest 1 orthogroups (O50 was 1). There were 0 orthogroups with all species present and 0 of these consisted entirely of single-copy genes.

2021-04-30 18:20:13 : Done orthogroups

Analysing Orthogroups
=====================

Calculating gene distances
--------------------------
2021-04-30 18:20:15 : Done
Using fallback species tree inference method
/Users/madelynschaut/miniconda3/lib/python3.8/site-packages/numpy/core/fromnumeric.py:3419: RuntimeWarning: Mean of empty slice.
  return _methods._mean(a, axis=axis, dtype=dtype,
/Users/madelynschaut/miniconda3/lib/python3.8/site-packages/numpy/core/_methods.py:188: RuntimeWarning: invalid value encountered in double_scalars
  ret = ret.dtype.type(ret / rcount)

Inferring gene and species trees
--------------------------------

Best outgroup(s) for species tree
---------------------------------
2021-04-30 18:20:18 : Starting STRIDE
Traceback (most recent call last):
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/stride.py", line 506, in GetRoot
    speciesTree = tree.Tree(speciesTreeFN, format=2)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/tree.py", line 221, in __init__
    read_newick(newick, root_node = self, format=format)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/newick.py", line 216, in read_newick
    raise NewickError('Unexisting tree file or Malformed newick tree structure.')
scripts_of.newick.NewickError: Unexisting tree file or Malformed newick tree structure.

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/madelynschaut/miniconda3/bin/orthofinder", line 7, in <module>
    main(args)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/__main__.py", line 1765, in main
    GetOrthologues(speciesInfoObj, options, prog_caller)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/__main__.py", line 1527, in GetOrthologues
    orthologues.OrthologuesWorkflow(speciesInfoObj.speciesToUse, 
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/orthologues.py", line 1039, in OrthologuesWorkflow
    roots, clusters_counter, rootedSpeciesTreeFN, nSupport, _, _, stride_dups = stride.GetRoot(spTreeFN_ids, files.FileHandler.GetOGsTreeDir(), stride.GeneToSpecies_dash, nHighParallel, qWriteRootedTree=True)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/stride.py", line 509, in GetRoot
    speciesTree = tree.Tree(speciesTreeFN, format=1)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/tree.py", line 221, in __init__
    read_newick(newick, root_node = self, format=format)
  File "/Users/madelynschaut/miniconda3/bin/scripts_of/newick.py", line 216, in read_newick
    raise NewickError('Unexisting tree file or Malformed newick tree structure.')
scripts_of.newick.NewickError: Unexisting tree file or Malformed newick tree structure.

```