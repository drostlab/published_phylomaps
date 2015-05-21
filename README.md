# A Collection of Published Phylostratigraphic Maps and Divergence Maps

The following studies include published `Phylostratigraphic Maps` and `Divergence Maps` based on similar approaches, but using different parameter sets.
This collection aims to store all published maps and furthermore, provides scripts for easy data retrieval to be able to integrate corresponding maps into a phylostranscriptomics workflow with [myTAI](https://github.com/HajkD/myTAI).

## [Tomislav Domazet-Lošo, Josip Brajković, Diethard Tautz, 2007](http://www.sciencedirect.com/science/article/pii/S0168952507002995)

__Title__: _A phylostratigraphy approach to uncover the genomic history of major adaptations in metazoan lineages_

This study introduced `Phylostratigraphy` as computational method to quantify gene age in terms of sequence homology resuting in an organism specific `Phylostratigraphic Map`.

Published `Phylostratigraphic Map`:

- __Organisms__: Drosophila melanogaster (fly)
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)

__Data sets are not avaiable as Supplementary Tables.__


## [Tomislav Domazet-Lošo and Diethard Tautz, 2008](http://mbe.oxfordjournals.org/content/25/12/2699)

__Title__: _An Ancient Evolutionary Origin of Genes Associated with Human Genetic Diseases_

Published `Phylostratigraphic Map`:

- __Organisms__: Homo sapiens (human); ENSEMBL version 45
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)
- __Splice variants__: always using the longest splice variant


Download Map using R:

```r
# download the Phylostratigraphic Map of Homo sapiens
# from Tomislav Domazet-Lošo and Diethard Tautz, 2008
download.file( url      = "http://mbe.oxfordjournals.org/content/suppl/2008/09/25/msn214.DC1/mbe-08-0522-File008_msn214.xls", 
               destfile = "MBE_2008_Homo_Sapiens_PhyloMap.xls" )
    
```

Read the `*.xls` file of the `Phylostratigraphic Map` of Homo sapiens and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
HomoSapiensPhyloMap.MBE <- read_excel("MBE_2008_Homo_Sapiens_PhyloMap.xls", sheet = 1,skip = 1)

# format Phylostratigraphic Map for use in myTAI
HomoSapiens.PhyloMap <- HomoSapiensPhyloMap.MBE[ , c("Phylostratum","Gene_ID")]

# have a look at the final format
head(HomoSapiens.PhyloMap)
```

```
  Phylostratum         Gene_ID
1            1 ENSG00000100053
2            1 ENSG00000100058
3            1 ENSG00000206066
4            1 ENSG00000100068
5            1 ENSG00000100077
6            1 ENSG00000133454
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Map` of Homo sapiens from [Domazet-Lošo and Tautz, 2008](http://mbe.oxfordjournals.org/content/25/12/2699) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).





