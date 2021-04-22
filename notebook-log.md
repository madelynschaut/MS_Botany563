# Notebook Log


## Bioconda
downloaded bioconda and followed installation instructions from https://bioconda.github.io/user/install.html


## ClustalW
downloaded ClustalW file clustalw-2.1-macosx from http://www.clustal.org/clustal2/ and copied to Desktop/software
copied ADH_grplantFeb19_OG0002122.fa to software folder and renamed to ADH_grplant_OG0002122.fa
opened the terminal 
```
cd desktop
cd software
ls
clustalw-2.1-macosx/clustalw2 -ALIGN -INFILE=ADH_grplant_OG0002122.fasta -OUTFILE=ADH_grplant_OG0002122-aligned.fasta -OUTPUT=PHYLIP
```
zsh: bad CPU type in executable: clustalw-2.1-macosx/clustalw2
```
conda activate
conda create -n clustalw2 -c biobuilds -y clustalw
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
conda activate clustalw2
clustalw2 -ALIGN -INFILE=ADH_grplant_OG0002122.fasta -OUTFILE=ADH_grplant_OG0002122-aligned.fasta -OUTPUT=PHYLIP
```
CLUSTAL 2.1 Multiple Sequence Alignments
...
PHYLIP-Alignment file created   [ADH_grplant_OG0002122-aligned.fasta]


## OrthoFinder
downloaded orthofinder and followed the steps outlined in https://davidemms.github.io/orthofinder_tutorials/downloading-and-running-orthofinder.html




