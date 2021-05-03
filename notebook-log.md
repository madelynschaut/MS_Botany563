# reproducible script for final project analysis

I cloned my madelynschaut/MS_Botany563 github repository to my local computer
```
pwd
git clone https://github.com/madelynschaut/MS_Botany563.git
cd MS_Botany563
open README.md
```

I used the following code to update github to changes in my local computer throughout the entire analysis
```
git add .
git commit -m "updated readme"
git push
```

## data for ADH enzymes in Caryophyllales

I copied one Arabidopsis thaliana ADH (AtADH) enzyme AT1G15710.1 sequence from Beth Moore's data "ADH_grplantFeb19_OG0002122.fasta"

I used BLASTp to search the AtADH AT1G15710.1 sequence to the order Caryophyllales (taxid:3524)
```
>AT1G15710.1
MLLHFSPAKPLISPPNLRRNSPTFLISPPRSLRIRAIDAAQIFDYETQLKSEYRKSSALKIAVLGFGNFGQFLSKTLIRH
GHDLITHSRSDYSDAANSIGARFFDNPHDLCEQHPDVVLLCTSILSTESVLRSFPFQRLRRSTLFVDVLSVKEFPKALFI
KYLPKEFDILCTHPMFGPESGKHSWSGLPFVYDKVRIGDAASRQERCEKFLRIFENEGCKMVEMSCEKHDYYAAGSQFVT
HTMGRVLEKYGVESSPINTKGYETLLDLVENTSSDSFELFYGLFMYNPNALEQLERLDMAFESVKKELFGRLHQQYRKQM
FGGEVQSPKKTEQKLLNDGGVVPMNDISSSSSSSSSSS*
```
I downloaded the entire BLAST job file "8SF1N9EW016-Alignment.txt"

I also downloaded the complete sequence file for sequences producing significant alignments "AtADH_caryophyllales_completesequence.txt". I added two Arabidopsis sequences and four sequences from another species: Amaranthus hypochondriacus from Beth's original data to make the final dataset.

This dataset consists of the following:
```
number of species = 20
number of genes = 36
```

Then, I made individual species .fasta files to run on OrthoFinder, files located in "species_files" folder in my software folder
```
1. Arabidopsis_thaliana
2. Amaranthus_hypochondriacus
3. Amaranthus_tricolor
4. Basella_alba
5. Beta_vulgaris
6. Chenopodium_quinoa
7. Corrigiola_litoralis
8. Herniaria_latifolia
9. Macarthuria_australis
10. Microtea_debilis
11. Mirabilis_jalapa
12. Nepenthes_ventricosaXalata
13. Paronychia_polygonifolia
14. Polycarpon_tetraphyllum
15. Portulaca_olerace
16. Rivina_humilis
17. Simmondsia_chinensis
18. Spergularia_marina
19. Spinacia_oleracea
20. Telephium_imperati
```

All raw data files are located in the 'Data' folder in my GitHub


## Bioconda
I downloaded bioconda and followed installation instructions from https://bioconda.github.io/user/install.html.
The GitHub repo for bioconda can be found here: https://github.com/bioconda/bioconda-recipes.

## OrthoFinder
I downloaded orthofinder v2.5.2 from https://davidemms.github.io/orthofinder_tutorials/downloading-and-running-orthofinder.html. The GitHub repo for orthofinder can be found here: https://github.com/davidemms/OrthoFinder.

### ran orthofinder through the terminal

I used bioconda to install orthofinder:
```
conda install -c bioconda orthofinder
```

The following was returned:
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

Then, to confirm if orthofider was correctly installed, I ran:
```
orthofinder -h
```

The following was returned:
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

So, it appears that orthofinder was successfully installed

I used a script provided with OrthoFinder to extract just the longest transcript variant per gene and run OrthoFinder on these files.
Python script is not installed during conda installation-- So, I needed to get the python scripts from the github repo:
```
cd ..
cd software
git clone https://github.com/davidemms/OrthoFinder.git
```

The following was returned:
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

I ran orthofinder on my individual species files
```
orthofinder -f species_files/
```

The following was returned:
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

A new file was created titled "OrthoFinder" with all of the summary statistics and orthogroup sequences

From this analysis, two orthogroups were generated: OG0000000.fa which contains 32 genes and OG0000001.fa which contains 4 genes (both genes from the species Chenopodium quinoa (XP_021760702.1 and XP_021741823.1); both genes from the species Macarthuria australis (AYE54619.1 and AYE54615.1))

I used only the OG0000000.fa orthogroup moving forward


## ClustalW
I downloaded ClustalW file clustalw-2.1-macosx from http://www.clustal.org/clustal2/ and copied to Desktop/software

### ran clustalW2 through the terminal
I attempted to run ClustalW v2.1.1 using the code:
```
clustalw-2.1-macosx/clustalw2 -ALIGN -INFILE=ADH_OG0000000.fa -OUTFILE=ADH_OG0000000-aligned.fasta -OUTPUT=FASTA
```

But, the following was returned:
```
zsh: bad CPU type in executable: clustalw-2.1-macosx/clustalw2
```

So, based off of Beth's advice in the class GitHub repo, I ran the following:
```
conda activate
conda create -n clustalw2 -c biobuilds -y clustalw
```

The following was returned:
```
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /Users/madelynschaut/miniconda3/envs/clustalw2

  added / updated specs:
    - clustalw


The following NEW packages will be INSTALLED:

  clustalw           biobuilds/osx-64::clustalw-2.1-1


Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate clustalw2
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

Then, I activated clustalw2 via conda and ran clustalw:
```
conda activate clustalw2
clustalw2 -ALIGN -INFILE=ADH_OG0000000.fa -OUTFILE=ADH_OG0000000-aligned.fasta -OUTPUT=FASTA
```

The following was returned:
```
 CLUSTAL 2.1 Multiple Sequence Alignments


Sequence format is Pearson
Sequence 1: AH020680-RA      401 aa
Sequence 2: AH013976-RA      229 aa
Sequence 3: AH013978-RA      363 aa
Sequence 4: AH013977-RA       66 aa
Sequence 5: QOY59747.1       398 aa
Sequence 6: AT1G15710.1      358 aa
Sequence 7: AT5G34930.1      640 aa
Sequence 8: AYE54618.1       344 aa
Sequence 9: AST12926.1       386 aa
Sequence 10: AST16042.1       386 aa
Sequence 11: AST12931.1       398 aa
Sequence 12: AST12935.1       407 aa
Sequence 13: XP_010687854.1   386 aa
Sequence 14: XP_010687851.1   398 aa
Sequence 15: ASA40298.1       358 aa
Sequence 16: AST14836.1       239 aa
Sequence 17: AYE54620.1       418 aa
Sequence 18: AYE54617.1       314 aa
Sequence 19: AMR60658.1       323 aa
Sequence 20: AST12937.1       321 aa
Sequence 21: AST14835.1       385 aa
Sequence 22: AYE54616.1       327 aa
Sequence 23: AST12940.1       341 aa
Sequence 24: AST12939.1       375 aa
Sequence 25: AYE54621.1       364 aa
Sequence 26: AYE54614.1       375 aa
Sequence 27: AST14834.1       396 aa
Sequence 28: XP_021849766.1   398 aa
Sequence 29: AST12936.1       321 aa
Sequence 30: AST12938.1       346 aa
Sequence 31: XP_021849779.1   399 aa
Sequence 32: ASA40299.1       329 aa
Start of Pairwise alignments
Aligning...

Sequences (1:2) Aligned. Score:  72
Sequences (1:3) Aligned. Score:  52
Sequences (1:4) Aligned. Score:  69
Sequences (1:5) Aligned. Score:  75
Sequences (1:6) Aligned. Score:  51
Sequences (1:7) Aligned. Score:  47
Sequences (1:8) Aligned. Score:  69
Sequences (1:9) Aligned. Score:  56
Sequences (1:10) Aligned. Score:  56
Sequences (1:11) Aligned. Score:  71
Sequences (1:12) Aligned. Score:  71
Sequences (1:13) Aligned. Score:  56
Sequences (1:14) Aligned. Score:  71
Sequences (1:15) Aligned. Score:  70
Sequences (1:16) Aligned. Score:  82
Sequences (1:17) Aligned. Score:  50
Sequences (1:18) Aligned. Score:  76
Sequences (1:19) Aligned. Score:  72
Sequences (1:20) Aligned. Score:  63
Sequences (1:21) Aligned. Score:  52
Sequences (1:22) Aligned. Score:  69
Sequences (1:23) Aligned. Score:  70
Sequences (1:24) Aligned. Score:  64
Sequences (1:25) Aligned. Score:  57
Sequences (1:26) Aligned. Score:  59
Sequences (1:27) Aligned. Score:  58
Sequences (1:28) Aligned. Score:  57
Sequences (1:29) Aligned. Score:  64
Sequences (1:30) Aligned. Score:  75
Sequences (1:31) Aligned. Score:  66
Sequences (1:32) Aligned. Score:  74
Sequences (2:3) Aligned. Score:  51
Sequences (2:4) Aligned. Score:  3
Sequences (2:5) Aligned. Score:  85
Sequences (2:6) Aligned. Score:  46
Sequences (2:7) Aligned. Score:  49
Sequences (2:8) Aligned. Score:  52
Sequences (2:9) Aligned. Score:  52
Sequences (2:10) Aligned. Score:  52
Sequences (2:11) Aligned. Score:  68
Sequences (2:12) Aligned. Score:  66
Sequences (2:13) Aligned. Score:  51
Sequences (2:14) Aligned. Score:  68
Sequences (2:15) Aligned. Score:  53
Sequences (2:16) Aligned. Score:  47
Sequences (2:17) Aligned. Score:  56
Sequences (2:18) Aligned. Score:  51
Sequences (2:19) Aligned. Score:  50
Sequences (2:20) Aligned. Score:  44
Sequences (2:21) Aligned. Score:  46
Sequences (2:22) Aligned. Score:  48
Sequences (2:23) Aligned. Score:  53
Sequences (2:24) Aligned. Score:  55
Sequences (2:25) Aligned. Score:  46
Sequences (2:26) Aligned. Score:  46
Sequences (2:27) Aligned. Score:  52
Sequences (2:28) Aligned. Score:  56
Sequences (2:29) Aligned. Score:  46
Sequences (2:30) Aligned. Score:  57
Sequences (2:31) Aligned. Score:  64
Sequences (2:32) Aligned. Score:  50
Sequences (3:4) Aligned. Score:  13
Sequences (3:5) Aligned. Score:  52
Sequences (3:6) Aligned. Score:  48
Sequences (3:7) Aligned. Score:  48
Sequences (3:8) Aligned. Score:  50
Sequences (3:9) Aligned. Score:  75
Sequences (3:10) Aligned. Score:  75
Sequences (3:11) Aligned. Score:  50
Sequences (3:12) Aligned. Score:  47
Sequences (3:13) Aligned. Score:  75
Sequences (3:14) Aligned. Score:  50
Sequences (3:15) Aligned. Score:  50
Sequences (3:16) Aligned. Score:  68
Sequences (3:17) Aligned. Score:  63
Sequences (3:18) Aligned. Score:  55
Sequences (3:19) Aligned. Score:  53
Sequences (3:20) Aligned. Score:  58
Sequences (3:21) Aligned. Score:  42
Sequences (3:22) Aligned. Score:  52
Sequences (3:23) Aligned. Score:  51
Sequences (3:24) Aligned. Score:  51
Sequences (3:25) Aligned. Score:  57
Sequences (3:26) Aligned. Score:  49
Sequences (3:27) Aligned. Score:  47
Sequences (3:28) Aligned. Score:  74
Sequences (3:29) Aligned. Score:  71
Sequences (3:30) Aligned. Score:  51
Sequences (3:31) Aligned. Score:  51
Sequences (3:32) Aligned. Score:  52
Sequences (4:5) Aligned. Score:  90
Sequences (4:6) Aligned. Score:  36
Sequences (4:7) Aligned. Score:  22
Sequences (4:8) Aligned. Score:  57
Sequences (4:9) Aligned. Score:  37
Sequences (4:10) Aligned. Score:  37
Sequences (4:11) Aligned. Score:  68
Sequences (4:12) Aligned. Score:  68
Sequences (4:13) Aligned. Score:  37
Sequences (4:14) Aligned. Score:  68
Sequences (4:15) Aligned. Score:  60
Sequences (4:16) Aligned. Score:  15
Sequences (4:17) Aligned. Score:  33
Sequences (4:18) Aligned. Score:  59
Sequences (4:19) Aligned. Score:  56
Sequences (4:20) Aligned. Score:  36
Sequences (4:21) Aligned. Score:  33
Sequences (4:22) Aligned. Score:  53
Sequences (4:23) Aligned. Score:  56
Sequences (4:24) Aligned. Score:  59
Sequences (4:25) Aligned. Score:  39
Sequences (4:26) Aligned. Score:  53
Sequences (4:27) Aligned. Score:  37
Sequences (4:28) Aligned. Score:  37
Sequences (4:29) Aligned. Score:  37
Sequences (4:30) Aligned. Score:  69
Sequences (4:31) Aligned. Score:  69
Sequences (4:32) Aligned. Score:  63
Sequences (5:6) Aligned. Score:  52
Sequences (5:7) Aligned. Score:  48
Sequences (5:8) Aligned. Score:  71
Sequences (5:9) Aligned. Score:  61
Sequences (5:10) Aligned. Score:  61
Sequences (5:11) Aligned. Score:  73
Sequences (5:12) Aligned. Score:  72
Sequences (5:13) Aligned. Score:  59
Sequences (5:14) Aligned. Score:  73
Sequences (5:15) Aligned. Score:  72
Sequences (5:16) Aligned. Score:  84
Sequences (5:17) Aligned. Score:  56
Sequences (5:18) Aligned. Score:  78
Sequences (5:19) Aligned. Score:  73
Sequences (5:20) Aligned. Score:  64
Sequences (5:21) Aligned. Score:  53
Sequences (5:22) Aligned. Score:  70
Sequences (5:23) Aligned. Score:  71
Sequences (5:24) Aligned. Score:  65
Sequences (5:25) Aligned. Score:  60
Sequences (5:26) Aligned. Score:  58
Sequences (5:27) Aligned. Score:  58
Sequences (5:28) Aligned. Score:  55
Sequences (5:29) Aligned. Score:  65
Sequences (5:30) Aligned. Score:  78
Sequences (5:31) Aligned. Score:  71
Sequences (5:32) Aligned. Score:  75
Sequences (6:7) Aligned. Score:  50
Sequences (6:8) Aligned. Score:  51
Sequences (6:9) Aligned. Score:  53
Sequences (6:10) Aligned. Score:  53
Sequences (6:11) Aligned. Score:  49
Sequences (6:12) Aligned. Score:  49
Sequences (6:13) Aligned. Score:  53
Sequences (6:14) Aligned. Score:  49
Sequences (6:15) Aligned. Score:  48
Sequences (6:16) Aligned. Score:  65
Sequences (6:17) Aligned. Score:  55
Sequences (6:18) Aligned. Score:  54
Sequences (6:19) Aligned. Score:  54
Sequences (6:20) Aligned. Score:  58
Sequences (6:21) Aligned. Score:  45
Sequences (6:22) Aligned. Score:  52
Sequences (6:23) Aligned. Score:  50
Sequences (6:24) Aligned. Score:  49
Sequences (6:25) Aligned. Score:  54
Sequences (6:26) Aligned. Score:  52
Sequences (6:27) Aligned. Score:  50
Sequences (6:28) Aligned. Score:  53
Sequences (6:29) Aligned. Score:  57
Sequences (6:30) Aligned. Score:  51
Sequences (6:31) Aligned. Score:  51
Sequences (6:32) Aligned. Score:  52
Sequences (7:8) Aligned. Score:  57
Sequences (7:9) Aligned. Score:  56
Sequences (7:10) Aligned. Score:  55
Sequences (7:11) Aligned. Score:  52
Sequences (7:12) Aligned. Score:  50
Sequences (7:13) Aligned. Score:  55
Sequences (7:14) Aligned. Score:  52
Sequences (7:15) Aligned. Score:  53
Sequences (7:16) Aligned. Score:  71
Sequences (7:17) Aligned. Score:  49
Sequences (7:18) Aligned. Score:  60
Sequences (7:19) Aligned. Score:  59
Sequences (7:20) Aligned. Score:  61
Sequences (7:21) Aligned. Score:  47
Sequences (7:22) Aligned. Score:  56
Sequences (7:23) Aligned. Score:  54
Sequences (7:24) Aligned. Score:  53
Sequences (7:25) Aligned. Score:  54
Sequences (7:26) Aligned. Score:  50
Sequences (7:27) Aligned. Score:  48
Sequences (7:28) Aligned. Score:  55
Sequences (7:29) Aligned. Score:  62
Sequences (7:30) Aligned. Score:  55
Sequences (7:31) Aligned. Score:  49
Sequences (7:32) Aligned. Score:  56
Sequences (8:9) Aligned. Score:  62
Sequences (8:10) Aligned. Score:  61
Sequences (8:11) Aligned. Score:  72
Sequences (8:12) Aligned. Score:  72
Sequences (8:13) Aligned. Score:  61
Sequences (8:14) Aligned. Score:  72
Sequences (8:15) Aligned. Score:  71
Sequences (8:16) Aligned. Score:  80
Sequences (8:17) Aligned. Score:  58
Sequences (8:18) Aligned. Score:  77
Sequences (8:19) Aligned. Score:  72
Sequences (8:20) Aligned. Score:  64
Sequences (8:21) Aligned. Score:  59
Sequences (8:22) Aligned. Score:  67
Sequences (8:23) Aligned. Score:  78
Sequences (8:24) Aligned. Score:  70
Sequences (8:25) Aligned. Score:  62
Sequences (8:26) Aligned. Score:  61
Sequences (8:27) Aligned. Score:  65
Sequences (8:28) Aligned. Score:  60
Sequences (8:29) Aligned. Score:  65
Sequences (8:30) Aligned. Score:  70
Sequences (8:31) Aligned. Score:  70
Sequences (8:32) Aligned. Score:  72
Sequences (9:10) Aligned. Score:  99
Sequences (9:11) Aligned. Score:  56
Sequences (9:12) Aligned. Score:  56
Sequences (9:13) Aligned. Score:  99
Sequences (9:14) Aligned. Score:  56
Sequences (9:15) Aligned. Score:  58
Sequences (9:16) Aligned. Score:  76
Sequences (9:17) Aligned. Score:  70
Sequences (9:18) Aligned. Score:  66
Sequences (9:19) Aligned. Score:  61
Sequences (9:20) Aligned. Score:  69
Sequences (9:21) Aligned. Score:  46
Sequences (9:22) Aligned. Score:  61
Sequences (9:23) Aligned. Score:  60
Sequences (9:24) Aligned. Score:  56
Sequences (9:25) Aligned. Score:  68
Sequences (9:26) Aligned. Score:  54
Sequences (9:27) Aligned. Score:  49
Sequences (9:28) Aligned. Score:  84
Sequences (9:29) Aligned. Score:  89
Sequences (9:30) Aligned. Score:  62
Sequences (9:31) Aligned. Score:  58
Sequences (9:32) Aligned. Score:  60
Sequences (10:11) Aligned. Score:  56
Sequences (10:12) Aligned. Score:  56
Sequences (10:13) Aligned. Score:  99
Sequences (10:14) Aligned. Score:  56
Sequences (10:15) Aligned. Score:  58
Sequences (10:16) Aligned. Score:  76
Sequences (10:17) Aligned. Score:  70
Sequences (10:18) Aligned. Score:  66
Sequences (10:19) Aligned. Score:  61
Sequences (10:20) Aligned. Score:  69
Sequences (10:21) Aligned. Score:  46
Sequences (10:22) Aligned. Score:  61
Sequences (10:23) Aligned. Score:  60
Sequences (10:24) Aligned. Score:  56
Sequences (10:25) Aligned. Score:  68
Sequences (10:26) Aligned. Score:  54
Sequences (10:27) Aligned. Score:  49
Sequences (10:28) Aligned. Score:  84
Sequences (10:29) Aligned. Score:  88
Sequences (10:30) Aligned. Score:  62
Sequences (10:31) Aligned. Score:  58
Sequences (10:32) Aligned. Score:  60
Sequences (11:12) Aligned. Score:  100
Sequences (11:13) Aligned. Score:  56
Sequences (11:14) Aligned. Score:  99
Sequences (11:15) Aligned. Score:  74
Sequences (11:16) Aligned. Score:  82
Sequences (11:17) Aligned. Score:  55
Sequences (11:18) Aligned. Score:  81
Sequences (11:19) Aligned. Score:  74
Sequences (11:20) Aligned. Score:  63
Sequences (11:21) Aligned. Score:  55
Sequences (11:22) Aligned. Score:  71
Sequences (11:23) Aligned. Score:  73
Sequences (11:24) Aligned. Score:  68
Sequences (11:25) Aligned. Score:  59
Sequences (11:26) Aligned. Score:  61
Sequences (11:27) Aligned. Score:  57
Sequences (11:28) Aligned. Score:  54
Sequences (11:29) Aligned. Score:  65
Sequences (11:30) Aligned. Score:  81
Sequences (11:31) Aligned. Score:  76
Sequences (11:32) Aligned. Score:  77
Sequences (12:13) Aligned. Score:  56
Sequences (12:14) Aligned. Score:  99
Sequences (12:15) Aligned. Score:  74
Sequences (12:16) Aligned. Score:  82
Sequences (12:17) Aligned. Score:  53
Sequences (12:18) Aligned. Score:  81
Sequences (12:19) Aligned. Score:  74
Sequences (12:20) Aligned. Score:  63
Sequences (12:21) Aligned. Score:  55
Sequences (12:22) Aligned. Score:  71
Sequences (12:23) Aligned. Score:  73
Sequences (12:24) Aligned. Score:  68
Sequences (12:25) Aligned. Score:  59
Sequences (12:26) Aligned. Score:  61
Sequences (12:27) Aligned. Score:  59
Sequences (12:28) Aligned. Score:  54
Sequences (12:29) Aligned. Score:  65
Sequences (12:30) Aligned. Score:  81
Sequences (12:31) Aligned. Score:  75
Sequences (12:32) Aligned. Score:  77
Sequences (13:14) Aligned. Score:  56
Sequences (13:15) Aligned. Score:  58
Sequences (13:16) Aligned. Score:  76
Sequences (13:17) Aligned. Score:  70
Sequences (13:18) Aligned. Score:  66
Sequences (13:19) Aligned. Score:  61
Sequences (13:20) Aligned. Score:  69
Sequences (13:21) Aligned. Score:  46
Sequences (13:22) Aligned. Score:  61
Sequences (13:23) Aligned. Score:  60
Sequences (13:24) Aligned. Score:  56
Sequences (13:25) Aligned. Score:  68
Sequences (13:26) Aligned. Score:  54
Sequences (13:27) Aligned. Score:  49
Sequences (13:28) Aligned. Score:  83
Sequences (13:29) Aligned. Score:  88
Sequences (13:30) Aligned. Score:  62
Sequences (13:31) Aligned. Score:  58
Sequences (13:32) Aligned. Score:  60
Sequences (14:15) Aligned. Score:  74
Sequences (14:16) Aligned. Score:  82
Sequences (14:17) Aligned. Score:  55
Sequences (14:18) Aligned. Score:  81
Sequences (14:19) Aligned. Score:  74
Sequences (14:20) Aligned. Score:  63
Sequences (14:21) Aligned. Score:  55
Sequences (14:22) Aligned. Score:  71
Sequences (14:23) Aligned. Score:  73
Sequences (14:24) Aligned. Score:  68
Sequences (14:25) Aligned. Score:  59
Sequences (14:26) Aligned. Score:  61
Sequences (14:27) Aligned. Score:  57
Sequences (14:28) Aligned. Score:  55
Sequences (14:29) Aligned. Score:  65
Sequences (14:30) Aligned. Score:  81
Sequences (14:31) Aligned. Score:  76
Sequences (14:32) Aligned. Score:  77
Sequences (15:16) Aligned. Score:  84
Sequences (15:17) Aligned. Score:  55
Sequences (15:18) Aligned. Score:  79
Sequences (15:19) Aligned. Score:  74
Sequences (15:20) Aligned. Score:  61
Sequences (15:21) Aligned. Score:  58
Sequences (15:22) Aligned. Score:  73
Sequences (15:23) Aligned. Score:  70
Sequences (15:24) Aligned. Score:  69
Sequences (15:25) Aligned. Score:  58
Sequences (15:26) Aligned. Score:  61
Sequences (15:27) Aligned. Score:  66
Sequences (15:28) Aligned. Score:  57
Sequences (15:29) Aligned. Score:  63
Sequences (15:30) Aligned. Score:  75
Sequences (15:31) Aligned. Score:  74
Sequences (15:32) Aligned. Score:  83
Sequences (16:17) Aligned. Score:  73
Sequences (16:18) Aligned. Score:  82
Sequences (16:19) Aligned. Score:  79
Sequences (16:20) Aligned. Score:  72
Sequences (16:21) Aligned. Score:  77
Sequences (16:22) Aligned. Score:  87
Sequences (16:23) Aligned. Score:  80
Sequences (16:24) Aligned. Score:  80
Sequences (16:25) Aligned. Score:  74
Sequences (16:26) Aligned. Score:  73
Sequences (16:27) Aligned. Score:  84
Sequences (16:28) Aligned. Score:  78
Sequences (16:29) Aligned. Score:  78
Sequences (16:30) Aligned. Score:  83
Sequences (16:31) Aligned. Score:  83
Sequences (16:32) Aligned. Score:  80
Sequences (17:18) Aligned. Score:  64
Sequences (17:19) Aligned. Score:  60
Sequences (17:20) Aligned. Score:  72
Sequences (17:21) Aligned. Score:  47
Sequences (17:22) Aligned. Score:  59
Sequences (17:23) Aligned. Score:  57
Sequences (17:24) Aligned. Score:  54
Sequences (17:25) Aligned. Score:  71
Sequences (17:26) Aligned. Score:  56
Sequences (17:27) Aligned. Score:  49
Sequences (17:28) Aligned. Score:  69
Sequences (17:29) Aligned. Score:  76
Sequences (17:30) Aligned. Score:  58
Sequences (17:31) Aligned. Score:  55
Sequences (17:32) Aligned. Score:  58
Sequences (18:19) Aligned. Score:  77
Sequences (18:20) Aligned. Score:  64
Sequences (18:21) Aligned. Score:  63
Sequences (18:22) Aligned. Score:  75
Sequences (18:23) Aligned. Score:  76
Sequences (18:24) Aligned. Score:  80
Sequences (18:25) Aligned. Score:  68
Sequences (18:26) Aligned. Score:  66
Sequences (18:27) Aligned. Score:  70
Sequences (18:28) Aligned. Score:  65
Sequences (18:29) Aligned. Score:  65
Sequences (18:30) Aligned. Score:  78
Sequences (18:31) Aligned. Score:  78
Sequences (18:32) Aligned. Score:  77
Sequences (19:20) Aligned. Score:  62
Sequences (19:21) Aligned. Score:  60
Sequences (19:22) Aligned. Score:  65
Sequences (19:23) Aligned. Score:  72
Sequences (19:24) Aligned. Score:  79
Sequences (19:25) Aligned. Score:  65
Sequences (19:26) Aligned. Score:  67
Sequences (19:27) Aligned. Score:  67
Sequences (19:28) Aligned. Score:  61
Sequences (19:29) Aligned. Score:  62
Sequences (19:30) Aligned. Score:  72
Sequences (19:31) Aligned. Score:  72
Sequences (19:32) Aligned. Score:  72
Sequences (20:21) Aligned. Score:  53
Sequences (20:22) Aligned. Score:  59
Sequences (20:23) Aligned. Score:  63
Sequences (20:24) Aligned. Score:  64
Sequences (20:25) Aligned. Score:  76
Sequences (20:26) Aligned. Score:  61
Sequences (20:27) Aligned. Score:  59
Sequences (20:28) Aligned. Score:  70
Sequences (20:29) Aligned. Score:  70
Sequences (20:30) Aligned. Score:  64
Sequences (20:31) Aligned. Score:  64
Sequences (20:32) Aligned. Score:  60
Sequences (21:22) Aligned. Score:  64
Sequences (21:23) Aligned. Score:  58
Sequences (21:24) Aligned. Score:  52
Sequences (21:25) Aligned. Score:  52
Sequences (21:26) Aligned. Score:  49
Sequences (21:27) Aligned. Score:  52
Sequences (21:28) Aligned. Score:  47
Sequences (21:29) Aligned. Score:  56
Sequences (21:30) Aligned. Score:  61
Sequences (21:31) Aligned. Score:  58
Sequences (21:32) Aligned. Score:  61
Sequences (22:23) Aligned. Score:  68
Sequences (22:24) Aligned. Score:  66
Sequences (22:25) Aligned. Score:  60
Sequences (22:26) Aligned. Score:  63
Sequences (22:27) Aligned. Score:  70
Sequences (22:28) Aligned. Score:  62
Sequences (22:29) Aligned. Score:  63
Sequences (22:30) Aligned. Score:  70
Sequences (22:31) Aligned. Score:  70
Sequences (22:32) Aligned. Score:  69
Sequences (23:24) Aligned. Score:  72
Sequences (23:25) Aligned. Score:  60
Sequences (23:26) Aligned. Score:  61
Sequences (23:27) Aligned. Score:  63
Sequences (23:28) Aligned. Score:  60
Sequences (23:29) Aligned. Score:  63
Sequences (23:30) Aligned. Score:  70
Sequences (23:31) Aligned. Score:  70
Sequences (23:32) Aligned. Score:  68
Sequences (24:25) Aligned. Score:  58
Sequences (24:26) Aligned. Score:  58
Sequences (24:27) Aligned. Score:  60
Sequences (24:28) Aligned. Score:  56
Sequences (24:29) Aligned. Score:  65
Sequences (24:30) Aligned. Score:  73
Sequences (24:31) Aligned. Score:  67
Sequences (24:32) Aligned. Score:  73
Sequences (25:26) Aligned. Score:  57
Sequences (25:27) Aligned. Score:  53
Sequences (25:28) Aligned. Score:  67
Sequences (25:29) Aligned. Score:  72
Sequences (25:30) Aligned. Score:  62
Sequences (25:31) Aligned. Score:  59
Sequences (25:32) Aligned. Score:  63
Sequences (26:27) Aligned. Score:  54
Sequences (26:28) Aligned. Score:  53
Sequences (26:29) Aligned. Score:  60
Sequences (26:30) Aligned. Score:  61
Sequences (26:31) Aligned. Score:  56
Sequences (26:32) Aligned. Score:  63
Sequences (27:28) Aligned. Score:  48
Sequences (27:29) Aligned. Score:  60
Sequences (27:30) Aligned. Score:  65
Sequences (27:31) Aligned. Score:  59
Sequences (27:32) Aligned. Score:  69
Sequences (28:29) Aligned. Score:  99
Sequences (28:30) Aligned. Score:  60
Sequences (28:31) Aligned. Score:  53
Sequences (28:32) Aligned. Score:  59
Sequences (29:30) Aligned. Score:  65
Sequences (29:31) Aligned. Score:  65
Sequences (29:32) Aligned. Score:  61
Sequences (30:31) Aligned. Score:  100
Sequences (30:32) Aligned. Score:  75
Sequences (31:32) Aligned. Score:  75
Guide tree file created:   [ADH_OG0000000.dnd]

There are 31 groups
Start of Multiple Alignment

Aligning...
Group 1: Sequences:   2      Score:4139
Group 2: Sequences:   2      Score:8625
Group 3: Sequences:   3      Score:8625
Group 4: Sequences:   5      Score:5014
Group 5: Sequences:   2      Score:1352
Group 6: Sequences:   2      Score:7526
Group 7: Sequences:   4      Score:1958
Group 8: Sequences:   9      Score:1970
Group 9: Sequences:   2      Score:6564
Group 10: Sequences:  11      Score:3901
Group 11: Sequences:   2      Score:6356
Group 12: Sequences:   3      Score:6055
Group 13: Sequences:  14      Score:4003
Group 14: Sequences:   2      Score:6596
Group 15: Sequences:  16      Score:4588
Group 16: Sequences:   2      Score:4881
Group 17: Sequences:   3      Score:5831
Group 18: Sequences:   4      Score:5989
Group 19: Sequences:  20      Score:4476
Group 20: Sequences:  21      Score:5036
Group 21: Sequences:   2      Score:8338
Group 22: Sequences:   3      Score:8335
Group 23: Sequences:   2      Score:6956
Group 24: Sequences:   5      Score:7167
Group 25: Sequences:   6      Score:6473
Group 26: Sequences:   7      Score:6482
Group 27: Sequences:   2      Score:6235
Group 28: Sequences:   9      Score:5799
Group 29: Sequences:   2      Score:5845
Group 30: Sequences:  11      Score:5293
Group 31: Sequences:  32      Score:4318
Alignment Score 588194
firstres = 1 lastres = 755
FASTA file created!

Fasta-Alignment file created    [ADH_OG0000000-aligned.fasta]
```


## RAxML-NG
I downloaded RAxML-NG v1.0.2 "64-bit OSX/macOS binary" from https://github.com/amkozlov/raxml-ng/

Then, I verified it installed correctly using:
```
raxml-ng -v
```

The following was returned:
```
RAxML-NG v. 1.0.2 released on 22.02.2021 by The Exelixis Lab.
Developed by: Alexey M. Kozlov and Alexandros Stamatakis.
Contributors: Diego Darriba, Tomas Flouri, Benoit Morel, Sarah Lutteropp, Ben Bettisworth.
Latest version: https://github.com/amkozlov/raxml-ng
Questions/problems/suggestions? Please visit: https://groups.google.com/forum/#!forum/raxml

System: Intel(R) Core(TM) i5-8257U CPU @ 1.40GHz, 4 cores, 8 GB RAM
```

Before running RAxML-NG, I need to determine best model for my data set using ModelTest-NG...

## ModelTest-NG

I cloned the git repo to my computer in order to install ModelTest-NG v0.1.7
```
git clone https://github.com/ddarriba/modeltest
```

The following was returned:
```
Cloning into 'modeltest'...
remote: Enumerating objects: 3226, done.
remote: Counting objects: 100% (133/133), done.
remote: Compressing objects: 100% (89/89), done.
remote: Total 3226 (delta 59), reused 96 (delta 40), pack-reused 3093
Receiving objects: 100% (3226/3226), 2.74 MiB | 7.12 MiB/s, done.
Resolving deltas: 100% (2588/2588), done.
```
Then, I installed a few more dependencies in order to run modeltest-ng on my computer following the steps from the same GitHub repo cited above

First, I installed homebrew from https://brew.sh/
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

The following was returned:
```
HEAD is now at eae355810 Merge pull request #11297 from Homebrew/dependabot/bundler/docs/rexml-3.2.5
==> Tapping homebrew/core
remote: Enumerating objects: 950888, done.
remote: Counting objects: 100% (488/488), done.
remote: Compressing objects: 100% (224/224), done.
remote: Total 950888 (delta 284), reused 456 (delta 264), pack-reused 950400
Receiving objects: 100% (950888/950888), 378.85 MiB | 1.12 MiB/s, done.
Resolving deltas: 100% (646778/646778), done.
```

I verified it installed correctly using:
```
brew
```

The following was returned:
```
Example usage:
  brew search TEXT|/REGEX/
  brew info [FORMULA|CASK...]
  brew install FORMULA|CASK...
  brew update
  brew upgrade [FORMULA|CASK...]
  brew uninstall FORMULA|CASK...
  brew list [FORMULA|CASK...]

Troubleshooting:
  brew config
  brew doctor
  brew install --verbose --debug FORMULA|CASK

Contributing:
  brew create URL [--no-fetch]
  brew edit [FORMULA|CASK...]

Further help:
  brew commands
  brew help [COMMAND]
  man brew
  https://docs.brew.sh
```

Second, I installed flex bison
```
brew install flex bison
```

The following was returned:
```
==> Downloading https://ghcr.io/v2/homebrew/core/gettext/manifests/0.21
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gettext/blobs/sha256:a025e143fe3f5f7e24a936b8b0a4926acfdd025b11d62
==> Downloading from https://pkg-containers-az.githubusercontent.com/ghcr1/blobs/sha256:a025e143fe3f5f7e24a936b8b0a
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/flex/manifests/2.6.4_2
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/flex/blobs/sha256:89ec2b04b1aab94297f490c60fe6ca2bcde7de9b76614827
==> Downloading from https://pkg-containers-az.githubusercontent.com/ghcr1/blobs/sha256:89ec2b04b1aab94297f490c60fe
######################################################################## 100.0%
==> Installing dependencies for flex: gettext
==> Installing flex dependency: gettext
==> Pouring gettext--0.21.big_sur.bottle.tar.gz
🍺  /usr/local/Cellar/gettext/0.21: 1,953 files, 19.8MB
==> Installing flex
==> Pouring flex--2.6.4_2.big_sur.bottle.tar.gz
==> Caveats
flex is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have flex first in your PATH, run:
  echo 'export PATH="/usr/local/opt/flex/bin:$PATH"' >> ~/.zshrc

For compilers to find flex you may need to set:
  export LDFLAGS="-L/usr/local/opt/flex/lib"
  export CPPFLAGS="-I/usr/local/opt/flex/include"

==> Summary
🍺  /usr/local/Cellar/flex/2.6.4_2: 46 files, 1.5MB
==> Downloading https://ghcr.io/v2/homebrew/core/bison/manifests/3.7.6-1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/bison/blobs/sha256:9f57b6c53d6595330adf79112e72034895f061769ebc890
==> Downloading from https://pkg-containers-az.githubusercontent.com/ghcr1/blobs/sha256:9f57b6c53d6595330adf79112e7
######################################################################## 100.0%
==> Pouring bison--3.7.6.big_sur.bottle.1.tar.gz
==> Caveats
bison is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have bison first in your PATH, run:
  echo 'export PATH="/usr/local/opt/bison/bin:$PATH"' >> ~/.zshrc

For compilers to find bison you may need to set:
  export LDFLAGS="-L/usr/local/opt/bison/lib"

==> Summary
🍺  /usr/local/Cellar/bison/3.7.6: 94 files, 3.3MB
==> Caveats
==> flex
flex is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have flex first in your PATH, run:
  echo 'export PATH="/usr/local/opt/flex/bin:$PATH"' >> ~/.zshrc

For compilers to find flex you may need to set:
  export LDFLAGS="-L/usr/local/opt/flex/lib"
  export CPPFLAGS="-I/usr/local/opt/flex/include"

==> bison
bison is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have bison first in your PATH, run:
  echo 'export PATH="/usr/local/opt/bison/bin:$PATH"' >> ~/.zshrc

For compilers to find bison you may need to set:
  export LDFLAGS="-L/usr/local/opt/bison/lib"
```

Third, I downloaded cmake from https://cmake.org/download/ for macOS 10.13 or later, and, in order to build modeltest-ng, I used the PTHREADS version steps.

I made a new build folder and set working directory for modeltest to run to:
```
mkdir build
cd build
```

Then, I ran the following in order to call cmake from where it was downloaded:
```
/Users/madelynschaut/desktop/Botany563_FinalProject/software/cmake-3.20.2-macos-universal/CMake.app/Contents/bin/cmake ..
```

The following was returned:
```
-- The C compiler identification is AppleClang 12.0.0.12000032
-- The CXX compiler identification is AppleClang 12.0.0.12000032
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /Library/Developer/CommandLineTools/usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /Library/Developer/CommandLineTools/usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Building RELEASE
-- Performing Test HAS_AVX
-- Performing Test HAS_AVX - Success
-- Performing Test HAS_SSE3
-- Performing Test HAS_SSE3 - Success
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE  
-- ModelTest Using flags:  -stdlib=libc++ -mmacosx-version-min=10.7 -mavx -D__AVX -DPTHREADS -pthread -D_NO_GUI_ 
-- ModelTest Compiler: AppleClang 12.0.0.12000032 => /Library/Developer/CommandLineTools/usr/bin/c++
-- pll-modules not found
-- Downloading pll-modules from https://github.com/ddarriba/pll-modules/archive/9333ffd14f34e503edcaca2cc6781a8fb597215a.zip
CMake Deprecation Warning at CMakeLists.txt:44 (cmake_minimum_required):
  Compatibility with CMake < 2.8.12 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done
-- Generating done
-- Build files have been written to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/modeltest/build/pll-modulesDownload
[ 11%] Creating directories for 'pll-modules'
[ 22%] Performing download step (download, verify and extract) for 'pll-modules'
-- Downloading...
   dst='/Users/madelynschaut/Desktop/Botany563_FinalProject/software/modeltest/build/pll-modulesDownload/pll-modules-prefix/src/9333ffd14f34e503edcaca2cc6781a8fb597215a.zip'
   timeout='none'
   inactivity timeout='none'
-- Using src='https://github.com/ddarriba/pll-modules/archive/9333ffd14f34e503edcaca2cc6781a8fb597215a.zip'
-- [download 100% complete]
-- Downloading... done
-- extracting...
     src='/Users/madelynschaut/desktop/Botany563_FinalProject/software/modeltest/build/pll-modulesDownload/pll-modules-prefix/src/9333ffd14f34e503edcaca2cc6781a8fb597215a.zip'
     dst='/Users/madelynschaut/desktop/Botany563_FinalProject/software/modeltest/libs/pll-modules'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 33%] No update step for 'pll-modules'
[ 44%] No patch step for 'pll-modules'
[ 55%] No configure step for 'pll-modules'
[ 66%] No build step for 'pll-modules'
[ 77%] No install step for 'pll-modules'
[ 88%] No test step for 'pll-modules'
[100%] Completed 'pll-modules'
[100%] Built target pll-modules
-- Finished downloading pll-modules
-- libpll not found
-- Downloading libpll from https://github.com/xflouris/libpll-2/archive/ffe25505677c73cce0b6555b850a2769a48e93f9.zip
CMake Deprecation Warning at CMakeLists.txt:44 (cmake_minimum_required):
  Compatibility with CMake < 2.8.12 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.

-- Configuring done
-- Generating done
-- Build files have been written to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/modeltest/build/libpllDownload
[ 11%] Creating directories for 'libpll'
[ 22%] Performing download step (download, verify and extract) for 'libpll'
-- Downloading...
   dst='/Users/madelynschaut/Desktop/Botany563_FinalProject/software/modeltest/build/libpllDownload/libpll-prefix/src/ffe25505677c73cce0b6555b850a2769a48e93f9.zip'
   timeout='none'
   inactivity timeout='none'
-- Using src='https://github.com/xflouris/libpll-2/archive/ffe25505677c73cce0b6555b850a2769a48e93f9.zip'
-- [download 100% complete]
-- Downloading... done
-- extracting...
     src='/Users/madelynschaut/desktop/Botany563_FinalProject/software/modeltest/build/libpllDownload/libpll-prefix/src/ffe25505677c73cce0b6555b850a2769a48e93f9.zip'
     dst='/Users/madelynschaut/desktop/Botany563_FinalProject/software/modeltest/libs/pll-modules/libs/libpll'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 33%] No update step for 'libpll'
[ 44%] No patch step for 'libpll'
[ 55%] No configure step for 'libpll'
[ 66%] No build step for 'libpll'
[ 77%] No install step for 'libpll'
[ 88%] No test step for 'libpll'
[100%] Completed 'libpll'
[100%] Built target libpll
-- Finished downloading libpll
CMake Deprecation Warning at libs/pll-modules/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 2.8.12 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- pll-modules static build enabled
CMake Deprecation Warning at libs/pll-modules/libs/libpll/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 2.8.12 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Found BISON: /usr/bin/bison (found version "2.3") 
-- Found FLEX: /usr/bin/flex (found version "2.5.35") 
-- SSE enabled. To disable it, run cmake with -DENABLE_SSE=false
-- AVX enabled. To disable it, run cmake with -DENABLE_AVX=false
-- AVX2 enabled. To disable it, run cmake with -DENABLE_AVX2=false
-- Libpll static build enabled
-- pll_static
CMake Deprecation Warning at libs/pll-modules/src/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 2.8.12 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Will compile pll-module optimize
-- Will compile pll-module algorithm
-- Will compile pll-module binary
-- Will compile pll-module msa
-- Will compile pll-module tree
-- Will compile pll-module util
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/madelynschaut/desktop/Botany563_FinalProject/software/modeltest/build
```

Then, I created "make"
```
make
```

The following was returned:
```
...
[100%] Linking CXX executable ../../bin/modeltest-ng
[100%] Built target modeltest_module
```
This means that modeltest-ng is in the bin folder inside of modeltest folder and it is ready to perform the model test on my data


### ran ModelTest-NG
I moved ADH_OG0000000-aligned.fasta to the "build" folder and ran the model test
```
/Users/madelynschaut/Desktop/Botany563_FinalProject/software/modeltest/bin/modeltest-ng -i ADH_OG0000000-aligned.fasta -t ml -d aa -p 2
```

The following was returned:
```

                             _      _ _            _      _   _  _____ 
                            | |    | | |          | |    | \ | |/ ____|
         _ __ ___   ___   __| | ___| | |_ ___  ___| |_   |  \| | |  __ 
        | '_ ` _ \ / _ \ / _` |/ _ \ | __/ _ \/ __| __|  | . ` | | |_ |
        | | | | | | (_) | (_| |  __/ | ||  __/\__ \ |_   | |\  | |__| |
        |_| |_| |_|\___/ \__,_|\___|_|\__\___||___/\__|  |_| \_|\_____|
--------------------------------------------------------------------------------
ModelTest-NG v0.1.7 released on 17.03.2021 by The Exelixis Lab.
Written by Diego Darriba.
Contributors: Tomas Flouri, Alexey Kozlov, Benoit Morel, David Posada, 
              Alexandros Stamatakis.
Latest version: https://github.com/ddarriba/modeltest
--------------------------------------------------------------------------------

Physical cores: 4
Logical cores:  8
Memory:         8GB
Extensions:     AVX

WARNING: MSA has not enough sites to infer reliable results
Creating new checkpoint file: ADH_OG0000000-aligned.fasta.ckp
--------------------------------------------------------------------------------
ModelTest-NG v0.1.7

Input data:
  MSA:        ADH_OG0000000-aligned.fasta
  Tree:       Maximum likelihood
    file:           -
  #taxa:            32
  #sites:           755
  #patterns:        437
  Max. thread mem:  32 MB

Output:
  Log:           ADH_OG0000000-aligned.fasta.log
  Starting tree: ADH_OG0000000-aligned.fasta.tree
  Results:       ADH_OG0000000-aligned.fasta.out

Selection options:
  # protein matrices: 19
  # protein models:   152
  include model parameters:
    Uniform:         true
    p-inv (+I):      true
    gamma (+G):      true
    both (+I+G):     true
    free rates (+R): false
    fixed freqs:     true
    estimated freqs: false
    #categories:     4
  gamma rates mode:   mean
  asc bias:           none
  epsilon (opt):      0.01
  epsilon (par):      0.05
  keep branches:      false

Additional options:
  verbosity:        very low
  threads:          2/4
  RNG seed:         12345
  subtree repeats:  enabled
--------------------------------------------------------------------------------
modeltest-ng was called as follows: 
>> /Users/madelynschaut/Desktop/Botany563_FinalProject/software/modeltest/bin/modeltest-ng -i ADH_OG0000000-aligned.fasta -t ml -d aa -p 2 


Partition 1/1

    3/152  DAYHOFF+I+G4+F 0h:00:24   0h:00:24          -11050.2462  0.7157  0.1003
    2/152  STMTREV+I+G4+F 0h:00:30   0h:00:30          -11225.0565  0.5201  0.0518
    4/152  FLU+I+G4+F     0h:00:22   0h:00:46          -11098.9707  0.5243  0.0341
    5/152  LG+I+G4+F      0h:00:22   0h:00:52          -11031.3054  0.5160  0.0216
    6/152  JTT-DCMUT+I+G4+F0h:00:21   0h:01:07          -10967.8475  0.7049  0.0891
    7/152  DCMUT+I+G4+F   0h:00:26   0h:01:18          -11050.3682  0.7157  0.1001
    8/152  HIVW+I+G4+F    0h:00:27   0h:01:34          -11218.2196  0.6330  0.0963
    9/152  JTT+I+G4+F     0h:00:23   0h:01:41          -10966.9491  0.7062  0.0899
   10/152  HIVB+I+G4+F    0h:00:25   0h:01:59          -11054.6820  0.6232  0.0901
   11/152  MTREV+I+G4+F   0h:00:24   0h:02:05          -11092.5743  0.6045  0.0790
   12/152  PMB+I+G4+F     0h:00:22   0h:02:21          -11106.2034  0.6078  0.0365
   13/152  WAG+I+G4+F     0h:00:23   0h:02:28          -11015.9252  0.5518  0.0222
   14/152  MTZOA+I+G4+F   0h:00:21   0h:02:42          -11128.9306  0.5068  0.0652
   15/152  RTREV+I+G4+F   0h:00:24   0h:02:52          -11076.3222  0.6652  0.0927
   17/152  CPREV+I+G4+F   0h:00:20   0h:03:12          -11056.0620  0.5157  0.0214
   16/152  MTART+I+G4+F   0h:00:34   0h:03:16          -11233.2313  0.4347  0.0366
   18/152  MTMAM+I+G4+F   0h:00:21   0h:03:33          -11183.0053  0.5068  0.0627
   19/152  VT+I+G4+F      0h:00:23   0h:03:39          -11025.2956  0.6838  0.0711
   20/152  BLOSUM62+I+G4+F0h:00:25   0h:03:58          -11111.1407  0.5666  0.0215
   21/152  STMTREV+G4+F   0h:00:29   0h:04:08          -11225.6176  0.4488       -
   22/152  PMB+G4+F       0h:00:20   0h:04:18          -11108.0794  0.5350       -
   23/152  DAYHOFF+G4+F   0h:00:20   0h:04:28          -11051.1651  0.5068       -
   24/152  LG+G4+F        0h:00:18   0h:04:36          -11030.9369  0.4722       -
   25/152  DCMUT+G4+F     0h:00:21   0h:04:49          -11051.3391  0.5068       -
   26/152  JTT+G4+F       0h:00:20   0h:04:56          -10966.5699  0.5068       -
   27/152  MTREV+G4+F     0h:00:18   0h:05:07          -11098.3420  0.4956       -
   28/152  WAG+G4+F       0h:00:18   0h:05:14          -11018.4454  0.5068       -
   29/152  RTREV+G4+F     0h:00:19   0h:05:26          -11077.5029  0.4909       -
   30/152  CPREV+G4+F     0h:00:19   0h:05:33          -11055.5528  0.5068       -
   31/152  VT+G4+F        0h:00:20   0h:05:46          -11027.0934  0.5350       -
   32/152  BLOSUM62+G4+F  0h:00:20   0h:05:53          -11110.7075  0.5390       -
   33/152  MTMAM+G4+F     0h:00:17   0h:06:03          -11187.8359  0.4294       -
   34/152  MTART+G4+F     0h:00:19   0h:06:12          -11236.3514  0.4172       -
   35/152  MTZOA+G4+F     0h:00:19   0h:06:22          -11131.9457  0.4345       -
   36/152  HIVB+G4+F      0h:00:20   0h:06:32          -11056.1958  0.4979       -
   38/152  JTT-DCMUT+G4+F 0h:00:19   0h:06:51          -10967.4546  0.5068       -
   37/152  HIVW+G4+F      0h:00:30   0h:06:52          -11220.4642  0.4884       -
   39/152  FLU+G4+F       0h:00:19   0h:07:10          -11098.6126  0.4710       -
   40/152  BLOSUM62+I+G4  0h:00:22   0h:07:14          -11202.8897  0.5541  0.0214
   41/152  VT+I+G4        0h:00:22   0h:07:32          -11079.9471  0.6483  0.0552
   42/152  DAYHOFF+I+G4   0h:00:23   0h:07:37          -11137.5998  0.7343  0.1042
   44/152  STMTREV+I+G4   0h:00:20   0h:07:57          -11422.3943  0.6459  0.1012
   43/152  MTART+I+G4     0h:00:27   0h:07:59          -11640.1076  0.5631  0.1402
   45/152  CPREV+I+G4     0h:00:20   0h:08:17          -11151.8033  0.5435  0.0217
   46/152  LG+I+G4        0h:00:20   0h:08:19          -11117.2140  0.5139  0.0212
   47/152  MTZOA+I+G4     0h:00:23   0h:08:40          -11451.9128  0.5647  0.1086
   48/152  FLU+I+G4       0h:00:26   0h:08:45          -11166.0684  0.5399  0.0466
   49/152  RTREV+I+G4     0h:00:23   0h:09:03          -11265.8403  0.6730  0.0928
   50/152  MTMAM+I+G4     0h:00:29   0h:09:14          -11617.4115  0.5350  0.1010
   51/152  PMB+I+G4       0h:00:22   0h:09:25          -11174.6413  0.5625  0.0220
   52/152  DCMUT+I+G4     0h:00:23   0h:09:37          -11137.6792  0.7367  0.1046
   53/152  WAG+I+G4       0h:00:23   0h:09:48          -11093.8671  0.5803  0.0245
   54/152  JTT-DCMUT+I+G4 0h:00:24   0h:10:01          -11031.3933  0.7045  0.0896
   55/152  HIVB+I+G4      0h:09:50   0h:19:38          -11233.1152  0.7157  0.1194
   56/152  JTT+I+G4       0h:09:43   0h:19:44          -11029.7940  0.7044  0.0901
   57/152  MTREV+I+G4     0h:00:19   0h:19:57          -11511.0940  0.6495  0.1064
   59/152  BLOSUM62+I+F   0h:00:05   0h:20:02          -11565.6399       -  0.2003
   58/152  HIVW+I+G4      0h:00:19   0h:20:03          -11473.8857  0.6917  0.1101
   60/152  VT+I+F         0h:00:06   0h:20:08          -11454.8961       -  0.2004
   61/152  MTMAM+I+F      0h:00:05   0h:20:08          -11923.1511       -  0.1987
   63/152  MTART+I+F      0h:00:06   0h:20:14          -12015.6287       -  0.1899
   62/152  CPREV+I+F      0h:00:07   0h:20:15          -11548.6137       -  0.1993
   64/152  RTREV+I+F      0h:00:05   0h:20:19          -11596.2355       -  0.2000
   65/152  MTZOA+I+F      0h:00:05   0h:20:20          -11805.0774       -  0.1984
   66/152  WAG+I+F        0h:00:06   0h:20:25          -11480.6096       -  0.2001
   67/152  PMB+I+F        0h:00:06   0h:20:26          -11556.9719       -  0.2004
   68/152  MTREV+I+F      0h:00:05   0h:20:30          -11644.7748       -  0.1989
   69/152  HIVB+I+F       0h:00:06   0h:20:32          -11641.7118       -  0.2009
   70/152  JTT+I+F        0h:00:05   0h:20:35          -11419.1666       -  0.2003
   71/152  HIVW+I+F       0h:00:05   0h:20:37          -11793.5416       -  0.2004
   72/152  DCMUT+I+F      0h:00:06   0h:20:41          -11541.3827       -  0.1997
   73/152  JTT-DCMUT+I+F  0h:00:05   0h:20:42          -11420.1781       -  0.2003
   74/152  LG+I+F         0h:00:05   0h:20:46          -11562.2837       -  0.2001
   75/152  FLU+I+F        0h:00:04   0h:20:46          -11730.5644       -  0.1989
   76/152  DAYHOFF+I+F    0h:00:06   0h:20:52          -11542.5148       -  0.1997
   77/152  STMTREV+I+F    0h:00:06   0h:20:52          -11761.3173       -  0.2004
   79/152  STMTREV+G4     0h:00:19   0h:21:11          -11424.2076  0.4751       -
   78/152  DAYHOFF+G4     0h:00:22   0h:21:14          -11139.3982  0.5350       -
   80/152  LG+G4          0h:00:18   0h:21:29          -11116.9462  0.4753       -
   81/152  FLU+G4         0h:00:25   0h:21:39          -11165.7640  0.4755       -
   82/152  DCMUT+G4       0h:00:22   0h:21:51          -11139.5095  0.5350       -
   83/152  JTT-DCMUT+G4   0h:00:18   0h:21:57          -11032.0820  0.5404       -
   84/152  JTT+G4         0h:00:19   0h:22:10          -11030.0963  0.5395       -
   85/152  HIVW+G4        0h:00:19   0h:22:16          -11476.0984  0.4885       -
   86/152  MTREV+G4       0h:00:20   0h:22:30          -11512.6123  0.4986       -
   87/152  HIVB+G4        0h:00:20   0h:22:36          -11233.8245  0.4924       -
   88/152  WAG+G4         0h:00:22   0h:22:52          -11093.5633  0.5428       -
   89/152  PMB+G4         0h:00:23   0h:22:59          -11174.2538  0.5350       -
   90/152  RTREV+G4       0h:08:44   0h:31:36          -11263.2357  0.5032       -
   91/152  MTZOA+G4       0h:08:46   0h:31:45          -11454.3601  0.4348       -
   92/152  CPREV+G4       0h:00:20   0h:31:56          -11151.4311  0.5068       -
   93/152  MTART+G4       0h:00:19   0h:32:04          -11645.8984  0.3943       -
   94/152  VT+G4          0h:00:22   0h:32:18          -11079.1787  0.5350       -
   95/152  MTMAM+G4       0h:00:20   0h:32:24          -11622.7645  0.4196       -
   97/152  VT+F           0h:00:02   0h:32:26          -11797.1659       -       -
   98/152  CPREV+F        0h:00:03   0h:32:29          -11864.3878       -       -
   99/152  BLOSUM62+F     0h:00:02   0h:32:31          -11901.9716       -       -
   96/152  BLOSUM62+G4    0h:00:14   0h:32:32          -11202.3700  0.5373       -
  100/152  RTREV+F        0h:00:02   0h:32:33          -11973.1191       -       -
  101/152  MTMAM+F        0h:00:01   0h:32:33          -12400.7781       -       -
  103/152  MTART+F        0h:00:02   0h:32:35          -12455.5529       -       -
  102/152  WAG+F          0h:00:02   0h:32:35          -11817.1081       -       -
  105/152  MTZOA+F        0h:00:02   0h:32:37          -12210.6487       -       -
  104/152  MTREV+F        0h:00:03   0h:32:38          -12029.6082       -       -
  106/152  JTT+F          0h:00:03   0h:32:40          -11784.0680       -       -
  107/152  PMB+F          0h:00:02   0h:32:40          -11897.6310       -       -
  109/152  HIVB+F         0h:00:01   0h:32:41          -12079.5814       -       -
  108/152  DCMUT+F        0h:00:02   0h:32:42          -11893.5904       -       -
  111/152  HIVW+F         0h:00:01   0h:32:43          -12213.3862       -       -
  110/152  LG+F           0h:00:03   0h:32:44          -11941.8033       -       -
  113/152  JTT-DCMUT+F    0h:00:01   0h:32:45          -11796.8592       -       -
  112/152  DAYHOFF+F      0h:00:02   0h:32:45          -11894.9319       -       -
  115/152  FLU+F          0h:00:01   0h:32:46          -12109.4255       -       -
  114/152  STMTREV+F      0h:00:02   0h:32:47          -12189.4448       -       -
  117/152  FLU+I          0h:00:04   0h:32:51          -11804.9159       -  0.1986
  116/152  STMTREV+I      0h:00:06   0h:32:52          -11930.3641       -  0.2005
  118/152  DAYHOFF+I      0h:00:06   0h:32:57          -11609.4237       -  0.1994
  119/152  JTT-DCMUT+I    0h:00:06   0h:32:58          -11479.9557       -  0.2001
  120/152  LG+I           0h:00:05   0h:33:02          -11650.9488       -  0.2000
  121/152  HIVW+I         0h:00:06   0h:33:04          -12078.2587       -  0.1997
  122/152  DCMUT+I        0h:00:06   0h:33:08          -11608.1661       -  0.1994
  123/152  HIVB+I         0h:00:05   0h:33:09          -11804.6467       -  0.2010
  124/152  JTT+I          0h:00:06   0h:33:14          -11478.9624       -  0.2002
  125/152  PMB+I          0h:00:06   0h:33:15          -11623.5597       -  0.2003
  126/152  MTREV+I        0h:00:05   0h:33:19          -12147.4094       -  0.1897
  127/152  MTZOA+I        0h:00:05   0h:33:20          -12253.0021       -  0.1886
  128/152  WAG+I          0h:00:06   0h:33:25          -11545.8230       -  0.2001
  129/152  MTART+I        0h:00:08   0h:33:28          -12594.9031       -  0.1878
  130/152  RTREV+I        0h:00:06   0h:33:31          -11774.7684       -  0.1996
  131/152  MTMAM+I        0h:00:05   0h:33:33          -12544.2554       -  0.1875
  132/152  CPREV+I        0h:00:06   0h:33:37          -11639.1482       -  0.1990
  133/152  BLOSUM62+I     0h:00:06   0h:33:39          -11655.2453       -  0.2003
  135/152  BLOSUM62       0h:00:02   0h:33:41          -11995.0419       -       -
  134/152  VT+I           0h:00:05   0h:33:42          -11509.7319       -  0.2004
  136/152  MTMAM          0h:00:02   0h:33:43          -13067.4754       -       -
  137/152  VT             0h:00:02   0h:33:44          -11856.3077       -       -
  138/152  MTART          0h:00:02   0h:33:45          -13101.3647       -       -
  140/152  MTZOA          0h:00:01   0h:33:46          -12711.5947       -       -
  139/152  CPREV          0h:00:02   0h:33:46          -11954.2880       -       -
  141/152  RTREV          0h:00:03   0h:33:49          -12143.9524       -       -
  142/152  PMB            0h:00:03   0h:33:49          -11967.8163       -       -
  144/152  HIVB           0h:00:01   0h:33:50          -12233.3201       -       -
  143/152  WAG            0h:00:01   0h:33:50          -11880.8601       -       -
  146/152  HIVW           0h:00:02   0h:33:52          -12466.9483       -       -
  145/152  MTREV          0h:00:02   0h:33:52          -12566.6826       -       -
  147/152  JTT            0h:00:02   0h:33:54          -11836.9016       -       -
  148/152  JTT-DCMUT      0h:00:02   0h:33:54          -11838.7250       -       -
  150/152  FLU            0h:00:01   0h:33:55          -12180.6323       -       -
  149/152  DCMUT          0h:00:02   0h:33:56          -11955.1135       -       -
  151/152  LG             0h:00:02   0h:33:57          -12029.4410       -       -
  152/152  STMTREV        0h:00:02   0h:33:58          -12367.8805       -       -
  153/152  DAYHOFF        0h:00:03   0h:34:00          -11956.4530       -       -
 ----ID---  ----MODEL---- ---Time--- -Elapsed--- -------LnL------- -Alpha- -P-inv-

Computation of likelihood scores completed. It took 0h:34:00

BIC       model              K            lnL          score          delta    weight
--------------------------------------------------------------------------------
       1  JTT+G4+F          20    -10966.5699     22469.9039         0.0000    0.4711
       2  JTT+G4             1    -11030.0963     22471.0491         1.1452    0.2657
       3  JTT-DCMUT+G4+F    20    -10967.4546     22471.6733         1.7694    0.1945
       4  JTT-DCMUT+G4       1    -11032.0820     22475.0205         5.1165    0.0365
       5  JTT+I+G4           2    -11029.7940     22477.0712         7.1673    0.0131
       6  JTT+I+G4+F        21    -10966.9491     22477.2890         7.3850    0.0117
       7  JTT-DCMUT+I+G4+F   21    -10967.8475     22479.0859         9.1819    0.0048
       8  JTT-DCMUT+I+G4     2    -11031.3933     22480.2699        10.3659    0.0026
       9  VT+G4              1    -11079.1787     22569.2139        99.3099    0.0000
      10  WAG+G4+F          20    -11018.4454     22573.6548       103.7509    0.0000
--------------------------------------------------------------------------------
Best model according to BIC
---------------------------
Model:              JTT+G4+F
lnL:                -10966.5699
Frequencies:        0.0579 0.0572 0.0462 0.0587 0.0181 0.0308 0.0581 0.0600 0.0326 0.0399 0.1145 0.0570 0.0270 0.0596 0.0451 0.0921 0.0539 0.0050 0.0237 0.0628
Inv. sites prop:    -
Gamma shape:        0.5068
Score:              22469.9039
Weight:             0.4711
---------------------------
Parameter importances
---------------------------
P.Inv:              0.0000
Gamma:              0.9678
Gamma-Inv:          0.0322
Frequencies:        0.6821
---------------------------
Model averaged estimates
---------------------------
P.Inv:              0.2002
Alpha:              0.5170
Alpha-P.Inv:        0.7052
P.Inv-Alpha:        0.0898
Frequencies:        0.0579 0.0572 0.0462 0.0587 0.0181 0.0308 0.0581 0.0600 0.0326 0.0399 0.1145 0.0570 0.0270 0.0596 0.0451 0.0921 0.0539 0.0050 0.0237 0.0628 

Commands:
  > phyml  -i ADH_OG0000000-aligned.fasta -d aa -m JTT -f e -v 0 -a e -c 4 -o tlr
  > raxmlHPC-SSE3 -s ADH_OG0000000-aligned.fasta -m PROTGAMMAJTTF -n EXEC_NAME -p PARSIMONY_SEED
  > raxml-ng --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F
  > paup -s ADH_OG0000000-aligned.fasta
  > iqtree -s ADH_OG0000000-aligned.fasta -m JTT+G4+F

AIC       model              K            lnL          score          delta    weight
--------------------------------------------------------------------------------
       1  JTT+G4+F          20    -10966.5699     22095.1398         0.0000    0.5659
       2  JTT-DCMUT+G4+F    20    -10967.4546     22096.9092         1.7694    0.2336
       3  JTT+I+G4+F        21    -10966.9491     22097.8981         2.7583    0.1425
       4  JTT-DCMUT+I+G4+F   21    -10967.8475     22099.6950         4.5552    0.0580
       5  JTT+G4             1    -11030.0963     22184.1926        89.0528    0.0000
       6  JTT+I+G4           2    -11029.7940     22185.5880        90.4482    0.0000
       7  JTT-DCMUT+G4       1    -11032.0820     22188.1640        93.0242    0.0000
       8  JTT-DCMUT+I+G4     2    -11031.3933     22188.7866        93.6468    0.0000
       9  WAG+I+G4+F        21    -11015.9252     22195.8504       100.7106    0.0000
      10  WAG+G4+F          20    -11018.4454     22198.8907       103.7509    0.0000
--------------------------------------------------------------------------------
Best model according to AIC
---------------------------
Model:              JTT+G4+F
lnL:                -10966.5699
Frequencies:        0.0579 0.0572 0.0462 0.0587 0.0181 0.0308 0.0581 0.0600 0.0326 0.0399 0.1145 0.0570 0.0270 0.0596 0.0451 0.0921 0.0539 0.0050 0.0237 0.0628
Inv. sites prop:    -
Gamma shape:        0.5068
Score:              22095.1398
Weight:             0.5659
---------------------------
Parameter importances
---------------------------
P.Inv:              0.0000
Gamma:              0.7995
Gamma-Inv:          0.2005
Frequencies:        1.0000
---------------------------
Model averaged estimates
---------------------------
P.Inv:              0.2003
Alpha:              0.5068
Alpha-P.Inv:        0.7059
P.Inv-Alpha:        0.0897
Frequencies:        0.0579 0.0572 0.0462 0.0587 0.0181 0.0308 0.0581 0.0600 0.0326 0.0399 0.1145 0.0570 0.0270 0.0596 0.0451 0.0921 0.0539 0.0050 0.0237 0.0628 

Commands:
  > phyml  -i ADH_OG0000000-aligned.fasta -d aa -m JTT -f e -v 0 -a e -c 4 -o tlr
  > raxmlHPC-SSE3 -s ADH_OG0000000-aligned.fasta -m PROTGAMMAJTTF -n EXEC_NAME -p PARSIMONY_SEED
  > raxml-ng --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F
  > paup -s ADH_OG0000000-aligned.fasta
  > iqtree -s ADH_OG0000000-aligned.fasta -m JTT+G4+F

AICc      model              K            lnL          score          delta    weight
--------------------------------------------------------------------------------
       1  JTT+G4+F          20    -10966.5699     22114.1398         0.0000    0.6143
       2  JTT-DCMUT+G4+F    20    -10967.4546     22115.9092         1.7694    0.2536
       3  JTT+I+G4+F        21    -10966.9491     22117.8981         3.7583    0.0938
       4  JTT-DCMUT+I+G4+F   21    -10967.8475     22119.6950         5.5552    0.0382
       5  JTT+G4             1    -11030.0963     22195.1926        81.0528    0.0000
       6  JTT+I+G4           2    -11029.7940     22196.5880        82.4482    0.0000
       7  JTT-DCMUT+G4       1    -11032.0820     22199.1640        85.0242    0.0000
       8  JTT-DCMUT+I+G4     2    -11031.3933     22199.7866        85.6468    0.0000
       9  WAG+I+G4+F        21    -11015.9252     22215.8504       101.7106    0.0000
      10  WAG+G4+F          20    -11018.4454     22217.8907       103.7509    0.0000
--------------------------------------------------------------------------------
Best model according to AICc
---------------------------
Model:              JTT+G4+F
lnL:                -10966.5699
Frequencies:        0.0579 0.0572 0.0462 0.0587 0.0181 0.0308 0.0581 0.0600 0.0326 0.0399 0.1145 0.0570 0.0270 0.0596 0.0451 0.0921 0.0539 0.0050 0.0237 0.0628
Inv. sites prop:    -
Gamma shape:        0.5068
Score:              22114.1398
Weight:             0.6143
---------------------------
Parameter importances
---------------------------
P.Inv:              0.0000
Gamma:              0.8680
Gamma-Inv:          0.1320
Frequencies:        1.0000
---------------------------
Model averaged estimates
---------------------------
P.Inv:              0.2003
Alpha:              0.5068
Alpha-P.Inv:        0.7059
P.Inv-Alpha:        0.0897
Frequencies:        0.0579 0.0572 0.0462 0.0587 0.0181 0.0308 0.0581 0.0600 0.0326 0.0399 0.1145 0.0570 0.0270 0.0596 0.0451 0.0921 0.0539 0.0050 0.0237 0.0628 

Commands:
  > phyml  -i ADH_OG0000000-aligned.fasta -d aa -m JTT -f e -v 0 -a e -c 4 -o tlr
  > raxmlHPC-SSE3 -s ADH_OG0000000-aligned.fasta -m PROTGAMMAJTTF -n EXEC_NAME -p PARSIMONY_SEED
  > raxml-ng --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F
  > paup -s ADH_OG0000000-aligned.fasta
  > iqtree -s ADH_OG0000000-aligned.fasta -m JTT+G4+F
Assertion failed: (tip_id != -1), function build_tips_recurse, file /Users/madelynschaut/desktop/Botany563_FinalProject/software/modeltest/libs/pll-modules/src/tree/consensus.c, line 954.
zsh: abort       -i ADH_OG0000000-aligned.fasta -t ml -d aa -p 2
```

According to the model test, the best fit for my data is the JTT+G4+F model

### ran RAxML-ng through the terminal
I followed the steps from https://biohpc.cornell.edu/doc/alignment_exercise3.html for most of this analysis

I ran my aligned data "ADH_OG0000000-aligned.fasta" from clustalw through RAxML-ng using the JTT+G4+F model. To verify in this file could be read by RAxML-NG, I ran the following check:
```
./raxml-ng --check --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F
```

The following was returned:
```
RAxML-NG was called at 30-Apr-2021 21:14:11 as follows:

./raxml-ng --check --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F

Analysis options:
  run mode: Alignment validation
  start tree(s): 
  random seed: 1619835251
  SIMD kernels: AVX2
  parallelization: coarse-grained (auto), PTHREADS (auto)

[00:00:00] Reading alignment from file: ADH_OG0000000-aligned.fasta
[00:00:00] Loaded alignment with 32 taxa and 755 sites

Alignment comprises 1 partitions and 755 sites

Partition 0: noname
Model: JTT+FC+G4m
Alignment sites: 755
Gaps: 52.45 %
Invariant sites: 52.72 %


Alignment can be successfully read by RAxML-NG.


Execution log saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/ADH_OG0000000-aligned.fasta.raxml.log

Analysis started: 30-Apr-2021 21:14:11 / finished: 30-Apr-2021 21:14:11

Elapsed time: 0.012 seconds
```
This means my file can be successfully read by RAxML-NG

***

### inferred ML trees


```
./raxml-ng --threads 2 --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F --prefix JTT
```

The following was returned:
```
Final LogLikelihood: -10964.422203

AIC score: 22090.844406 / AICc score: 22110.582890 / BIC score: 22465.608543
Free parameters (model + branch lengths): 81

WARNING: Best ML tree contains 1 near-zero branches!

Best ML tree with collapsed near-zero branches saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT.raxml.bestTreeCollapsed
Best ML tree saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT.raxml.bestTree
All ML trees saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT.raxml.mlTrees
Optimized model saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT.raxml.bestModel

Execution log saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT.raxml.log

Analysis started: 30-Apr-2021 21:19:14 / finished: 30-Apr-2021 21:22:06

Elapsed time: 172.561 seconds
```

### bootstrapping and branch support
the previous execution generated 20 ML trees by raxml-ng default settings. bootstrap support values will be generated for those trees

ran bootstrap on my aligned data ADH_OG0000000-aligned.fasta
```
./raxml-ng  --bootstrap --threads 2 --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F --prefix JTT_2
```

the following was returned:
```
RAxML-NG was called at 30-Apr-2021 21:56:07 as follows:

./raxml-ng --bootstrap --threads 2 --msa ADH_OG0000000-aligned.fasta --model JTT+G4+F --prefix JTT_2

Analysis options:
  run mode: Bootstrapping
  start tree(s): 
  bootstrap replicates: max: 1000 + bootstopping (autoMRE, cutoff: 0.030000)
  random seed: 1619837767
  tip-inner: OFF
  pattern compression: ON
  per-rate scalers: OFF
  site repeats: ON
  branch lengths: proportional (ML estimate, algorithm: NR-FAST)
  SIMD kernels: AVX2
  parallelization: coarse-grained (auto), PTHREADS (2 threads), thread pinning: OFF

[00:00:00] Reading alignment from file: ADH_OG0000000-aligned.fasta
[00:00:00] Loaded alignment with 32 taxa and 755 sites

Alignment comprises 1 partitions and 437 patterns

Partition 0: noname
Model: JTT+FC+G4m
Alignment sites / patterns: 755 / 437
Gaps: 52.45 %
Invariant sites: 52.72 %


NOTE: Binary MSA file created: JTT_2.raxml.rba

Parallelization scheme autoconfig: 1 worker(s) x 2 thread(s)

Parallel reduction/worker buffer size: 1 KB  / 0 KB

[00:00:00] Data distribution: max. partitions/sites/weight per thread: 1 / 219 / 17520
[00:00:00] Data distribution: max. searches per worker: 1000
[00:00:00] Starting bootstrapping analysis with 1000 replicates.

[00:00:06] Bootstrap tree #1, logLikelihood: -10092.968324
...
[11:48:43] Bootstrap tree #850, logLikelihood: -11445.661791
[11:48:44] Bootstrapping converged after 850 replicates.

Bootstrap trees saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT_2.raxml.bootstraps

Execution log saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT_2.raxml.log

Analysis started: 30-Apr-2021 21:56:07 / finished: 01-May-2021 09:44:51

Elapsed time: 42524.126 seconds
```

ran bootstrap to map values on the best ML tree
```
./raxml-ng --support --tree JTT.raxml.bestTree --bs-trees JTT_2.raxml.bootstraps --prefix JTT_3
```

the following was returned:
```
RAxML-NG was called at 01-May-2021 09:51:28 as follows:

./raxml-ng --support --tree JTT.raxml.bestTree --bs-trees JTT_2.raxml.bootstraps --prefix JTT_3

Analysis options:
  run mode: Compute bipartition support (Felsenstein Bootstrap)
  start tree(s): user
  random seed: 1619880688
  SIMD kernels: AVX2
  parallelization: coarse-grained (auto), PTHREADS (auto)

Reading reference tree from file: JTT.raxml.bestTree
Reference tree size: 32

Reading bootstrap trees from file: JTT_2.raxml.bootstraps
Loaded 850 trees with 32 taxa.

Best ML tree with Felsenstein bootstrap (FBP) support values saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT_3.raxml.support

Execution log saved to: /Users/madelynschaut/Desktop/Botany563_FinalProject/software/raxml-ng/JTT_3.raxml.log

Analysis started: 01-May-2021 09:51:28 / finished: 01-May-2021 09:51:28

Elapsed time: 0.079 seconds
```


## FigTree
I downloaded FigTree v1.4.4 from https://github.com/rambaut/figtree/releases. The GitHub repo for FigTree can be found here: https://github.com/rambaut/figtree.

I used figtree application to visualize the best ML tree generated from RAxML-NG

