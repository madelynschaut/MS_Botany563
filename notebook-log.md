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

copied ADH_grplantFeb19_OG0002122.fasta to software folder and renamed to ADH_grplant_OG0002122.fasta

ran clustalW2 through the terminal-- see "clustalW_script.md" for reproducible script


## OrthoFinder
downloaded orthofinder from https://davidemms.github.io/orthofinder_tutorials/downloading-and-running-orthofinder.html
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
...
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








