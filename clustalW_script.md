# clustalW script from the terminal
```
pwd
cd desktop
cd software
clustalw-2.1-macosx/clustalw2 -ALIGN -INFILE=ADH_OG0000000.fa -OUTFILE=ADH_OG0000000-aligned.fasta -OUTPUT=FASTA
```

the following was returned:
```
bad CPU type in executable: clustalw-2.1-macosx/clustalw2
```

ran this code based off of Beth's suggestion in the GitHub repo:
```
conda activate
conda create -n clustalw2 -c biobuilds -y clustalw
```

the following was returned:
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

activated clustalw2 via conda and ran clustalw:
```
conda activate clustalw2
clustalw2 -ALIGN -INFILE=ADH_OG0000000.fa -OUTFILE=ADH_OG0000000-aligned.fasta -OUTPUT=FASTA
```

the following was returned:
***