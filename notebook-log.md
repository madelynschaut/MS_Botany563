# Notebook Log

cloned my madelynschaut/MS_Botany563 github repository to my local computer
```
pwd
git clone https://github.com/madelynschaut/MS_Botany563.git
cd MS_Botany563
open README.md
```

to update github to changes in my local repo
```
git add .
git commit -m "updated readme"
git push
```

## Bioconda
downloaded bioconda and followed installation instructions from https://bioconda.github.io/user/install.html


## ClustalW
downloaded ClustalW file clustalw-2.1-macosx from http://www.clustal.org/clustal2/ and copied to Desktop/software
copied ADH_grplantFeb19_OG0002122.fa to software folder and renamed to ADH_grplant_OG0002122.fasta
opened the terminal 
```
cd desktop
cd software
ls
clustalw-2.1-macosx/clustalw2 -ALIGN -INFILE=ADH_grplant_OG0002122.fasta -OUTFILE=ADH_grplant_OG0002122-aligned.fasta -OUTPUT=PHYLIP

#return
zsh: bad CPU type in executable: clustalw-2.1-macosx/clustalw2

conda activate
conda create -n clustalw2 -c biobuilds -y clustalw

#return
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


conda activate clustalw2
clustalw2 -ALIGN -INFILE=ADH_grplant_OG0002122.fasta -OUTFILE=ADH_grplant_OG0002122-aligned.fasta -OUTPUT=PHYLIP

#return
CLUSTAL 2.1 Multiple Sequence Alignments
...
Guide tree file created:   [ADH_grplant_OG0002122.dnd]
Alignment Score 6470036
...
PHYLIP-Alignment file created   [ADH_grplant_OG0002122-aligned.fasta]
```

## OrthoFinder
downloaded orthofinder from https://davidemms.github.io/orthofinder_tutorials/downloading-and-running-orthofinder.html
```
conda install -c bioconda orthofinder

#return
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /Users/madelynschaut/miniconda3/envs/clustalw2

  added / updated specs:
    - orthofinder
...
Preparing transaction: done
Verifying transaction: done
Executing transaction: done

orthofinder -

#return
OrthoFinder version 2.5.2 Copyright (C) 2014 David Emms
...



