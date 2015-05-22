# A Collection of Published Phylostratigraphic Maps and Divergence Maps

The following studies include published `Phylostratigraphic Maps` and `Divergence Maps` based on similar approaches, but using different parameter sets.
This collection aims to store all published maps and furthermore, provides scripts for easy data retrieval to be able to integrate corresponding maps into a phylostranscriptomics workflow with [myTAI](https://github.com/HajkD/myTAI).

The [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) Vignette introduces the integration of the following `Phylostratigraphic Maps` and `Divergence Maps` to perform custom phylotranscriptomic analyses.

## [Tomislav Domazet-Lošo, Josip Brajković, Diethard Tautz, 2007](http://www.sciencedirect.com/science/article/pii/S0168952507002995)

__Title__: _A phylostratigraphy approach to uncover the genomic history of major adaptations in metazoan lineages_

This study introduced `Phylostratigraphy` as computational method to quantify gene age in terms of sequence homology resuting in an organism specific `Phylostratigraphic Map`.

Published `Phylostratigraphic Map`:

- __Organisms__: _Drosophila melanogaster_ (fly)
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)

__Data sets are not avaiable as Supplementary Tables.__


## [Tomislav Domazet-Lošo and Diethard Tautz, 2008](http://mbe.oxfordjournals.org/content/25/12/2699)

__Title__: _An Ancient Evolutionary Origin of Genes Associated with Human Genetic Diseases_

Published `Phylostratigraphic Map`:

- __Organisms__: _Homo sapiens_ (human); ENSEMBL version 45
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

Read the `*.xls` file storing the `Phylostratigraphic Map` of Homo sapiens and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
HomoSapiensPhyloMap.MBE <- read_excel("MBE_2008_Homo_Sapiens_PhyloMap.xls", sheet = 1, skip = 1)

# format Phylostratigraphic Map for use with myTAI
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



## [Tomislav Domazet-Lošo and Diethard Tautz, 2010](http://www.biomedcentral.com/1741-7007/8/66)

__Title__: _Phylostratigraphic tracking of cancer genes suggests a link to the emergence of multicellularity in metazoa_

Published `Phylostratigraphic Map`:

- __Organisms__: _Homo sapiens_ (human); based on 20,259 unique proteins published [here](http://www.sciencemag.org/content/321/5897/1801)
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)
- __Splice variants__: always using the longest splice variant


Download Map using R:

```r
# download the Phylostratigraphic Map of Homo sapiens
# from Domazet-Lošo and Tautz, 2010
download.file( url      = "http://www.biomedcentral.com/content/supplementary/1741-7007-8-66-s1.xls", 
               destfile = "BMCBiology_2010_Homo_Sapiens_PhyloMap.xls" )
    
```

Read the `*.xls` file storing the `Phylostratigraphic Map` of Homo sapiens and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
HomoSapiensPhyloMap.BMCBiology <- read_excel("BMCBiology_2010_Homo_Sapiens_PhyloMap.xls", sheet = 1, skip = 3, col_names = FALSE)

colnames(HomoSapiensPhyloMap.BMCBiology)[1:2] <- c("Gene_ID","Phylostratum")

# format Phylostratigraphic Map for use with myTAI
HomoSapiens.PhyloMap <- HomoSapiensPhyloMap.BMCBiology[ , c("Phylostratum","Gene_ID")]

# have a look at the final format
head(HomoSapiens.PhyloMap)
```

```
  Phylostratum      Gene_ID
1            1       15E1.2
2            1       3'HEXO
3            1 A0PJW7_HUMAN
4            1        A2BP1
5            1          A2M
6            1      A3GALT2
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Map` of Homo sapiens from [Domazet-Lošo and Tautz, 2010](http://www.biomedcentral.com/1741-7007/8/66) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).


## [Marcel Quint, Hajk-Georg Drost, Alexander Gabel, Kristian Karsten Ullrich,	Markus Boenn, Ivo Grosse, 2012](http://www.nature.com/nature/journal/v490/n7418/full/nature11394.html)

__Title__: _A transcriptomic hourglass in plant embryogenesis_

Published `Phylostratigraphic Map`:

- __Organisms__: _Arabidopsis thaliana_ 
- __E-value cutoff__: 1E-5 (blastp; protein sequences) 
- __Sequence type__: Protein Sequences
- __Reference data bases__: NCBI nr + additional plant genomes (phytozome)
- __Splice variants__: always using the longest splice variant

Published `KaKs Maps`:

- __Organisms__: _Arabidopsis thaliana_ versus _Arabidopsis lyrata_; _Arabidopsis thaliana_ versus _Brassica rapa_; _Arabidopsis thaliana_ versus _Capsella rubella_; _Arabidopsis thaliana_ versus _Thelungiella halophila_
- __E-value cutoff__: 1E-5 (blastp - best hit; protein sequences) 
- __Sequence type__: CDS + Protein Sequences

Download `Phylostratigraphic Map` using R:

```r
# download the Phylostratigraphic Map of Arabidopsis thaliana
# from Quint et al., 2012
download.file( url      = "http://www.nature.com/nature/journal/v490/n7418/extref/nature11394-s2.xls", 
               destfile = "Nature_2012_Arabidopsis_thaliana_PhyloMap.xls" )
    
```

Read the `*.xls` file storing the `Phylostratigraphic Map` of Arabidopsis thaliana and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
ArabidopsisThalianaPhyloMap.Nature <- read_excel("Nature_2012_Arabidopsis_thaliana_PhyloMap.xls", sheet = 1)

# format Phylostratigraphic Map of Arabidopsis thaliana for use with myTAI
ArabidopsisThaliana.PhyloMap <- ArabidopsisThalianaPhyloMap.Nature[ , 1:2]

# have a look at the final format
head(ArabidopsisThaliana.PhyloMap)
```

```
  Phylostratum      Gene
1           13 At5g15420
2           13 At2g07719
3           13 At3g43940
4           13 At5g45095
5           13 At5g60260
6           13 At1g54420
```


Download `KaKs Maps` using R:

```r
# download the KaKs Maps of Arabidopsis thaliana
# from Quint et al., 2012
download.file( url      = "http://www.nature.com/nature/journal/v490/n7418/extref/nature11394-s3.xls", 
               destfile = "Nature_2012_Arabidopsis_thaliana_KaKsMaps.xls" )
```    


### _Arabidopsis thaliana_ versus _Arabidopsis lyrata_

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
Ath_vs_Aly_KaKsMap.Nature <- read_excel("Nature_2012_Arabidopsis_thaliana_KaKsMaps.xls", sheet = 1)

# format KaKs Map of Arabidopsis thaliana versus Arabidopsis lyrata for use with myTAI
Ath_vs_Aly.KaKsMap <- Ath_vs_Aly_KaKsMap.Nature[ , 1:2]

# have a look at the final format
head(Ath_vs_Aly.KaKsMap)
```

```
     KaKs      Gene
1 0.18560 At5g53110
2 0.58980 At2g02320
3 0.07699 At5g14980
4 0.60110 At2g26050
5 0.08910 At4g17650
6 0.23650 At5g20040
```

### _Arabidopsis thaliana_ versus _Brassica rapa_

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
Ath_vs_Bra_KaKsMap.Nature <- read_excel("Nature_2012_Arabidopsis_thaliana_KaKsMaps.xls", sheet = 2)

# format KaKs Map of Arabidopsis thaliana versus Brassica rapa for use with myTAI
Ath_vs_Bra.KaKsMap <- Ath_vs_Bra_KaKsMap.Nature[ , 1:2]

# have a look at the final format
head(Ath_vs_Bra.KaKsMap)
```

```
     KaKs      Gene
1 0.22660 At5g53110
2 0.08425 At5g14980
3 0.32040 At2g26050
4 0.24060 At4g17650
5 0.29970 At5g20040
6 0.43220 At4g19750
```



### _Arabidopsis thaliana_ versus _Capsella rubella_

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
Ath_vs_Crub_KaKsMap.Nature <- read_excel("Nature_2012_Arabidopsis_thaliana_KaKsMaps.xls", sheet = 3)

# format KaKs Map of Arabidopsis thaliana versus Capsella rubella for use with myTAI
Ath_vs_Crub.KaKsMap <- Ath_vs_Crub_KaKsMap.Nature[ , 1:2]

# have a look at the final format
head(Ath_vs_Crub.KaKsMap)
```

```
     KaKs      Gene
1 0.41030 At1g01010
2 0.50510 At1g01020
3 0.13300 At1g01030
4 0.10300 At1g01040
5 0.04453 At1g01050
6 0.27210 At1g01060
```

### _Arabidopsis thaliana_ versus _Thelungiella halophila_

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
Ath_vs_Thal_KaKsMap.Nature <- read_excel("Nature_2012_Arabidopsis_thaliana_KaKsMaps.xls", sheet = 4)

# format KaKs Map of Arabidopsis thaliana versus Thelungiella halophila for use with myTAI
Ath_vs_Thal.KaKsMap <- Ath_vs_Thal_KaKsMap.Nature[ , 1:2]

# have a look at the final format
head(Ath_vs_Thal.KaKsMap)
```

```
     KaKs      Gene
1 0.54110 At1g01010
2 0.37860 At1g01020
3 0.10400 At1g01030
4 0.11070 At1g01040
5 0.01867 At1g01050
6 0.36660 At1g01060
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Map` and `KaKs Maps` of Arabidopsis thaliana from [Quint et al., 2012](http://www.nature.com/nature/journal/v490/n7418/full/nature11394.html) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).


## [Rafik Neme and Diethard Tautz, 2013](http://www.biomedcentral.com/1471-2164/14/117)

__Title__: _Phylogenetic patterns of emergence of new genes support a model of frequent de novo evolution_

Published `Phylostratigraphic Map`:

- __Organisms__: _Mus musculus_ (Ensembl v. 66), _Homo sapiens_ (Ensembl v. 68), _Danio rerio_ (Ensembl v. 68), _Gasterosteus aculeatus_ (Ensembl v. 68)
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)
- __Splice variants__: always using the longest splice variant


Download Map using R:

```r
# download the Phylostratigraphic Maps
# from Neme and Tautz, 2013
download.file( url      = "http://www.biomedcentral.com/content/supplementary/1471-2164-14-117-s1.xlsx", 
               destfile = "BMCGenomics_2013_species_PhyloMaps.xlsx" )
    
```

Read the `*.xlsx` file storing the `Phylostratigraphic Maps` of _Mus musculus_, _Homo sapiens_, _Danio rerio_, and _Gasterosteus aculeatus_ and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

### _Mus musculus_
```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file: Mus musculus
MusMusculusPhyloMap.BMCGenomics <- read_excel("BMCGenomics_2013_species_PhyloMaps.xlsx", sheet = 1)

# format Phylostratigraphic Map of Mus musculus for use with myTAI
MusMusculus.PhyloMap <- MusMusculusPhyloMap.BMCGenomics[ , c(2,1)]

# have a look at the final format
head(MusMusculus.PhyloMap)
```

```
  Oldest Phylostratum    Ensembl Gene ID
1                   1 ENSMUSG00000074155
2                   1 ENSMUSG00000086875
3                   1 ENSMUSG00000006948
4                   1 ENSMUSG00000079344
5                   1 ENSMUSG00000055193
6                   1 ENSMUSG00000004789
```

### _Homo sapiens_

```r

# read the excel file: Homo sapiens
HomoSapiensPhyloMap.BMCGenomics <- read_excel("BMCGenomics_2013_species_PhyloMaps.xlsx", sheet = 2)

# format Phylostratigraphic Map of Homo sapiens for use with myTAI
HomoSapiens.PhyloMap <- HomoSapiensPhyloMap.BMCGenomics[ , c(2,1)]

# have a look at the final format
head(HomoSapiens.PhyloMap)
```

```
  Oldest Phylostratum Ensembl Gene ID
1                   1 ENSG00000004059
2                   1 ENSG00000004478
3                   1 ENSG00000003137
4                   1 ENSG00000003509
5                   1 ENSG00000001036
6                   1 ENSG00000002587
```

### _Danio rerio_

```r

# read the excel file: Danio rerio
DanioRerioPhyloMap.BMCGenomics <- read_excel("BMCGenomics_2013_species_PhyloMaps.xlsx", sheet = 3)

# format Phylostratigraphic Map of Danio rerio for use with myTAI
DanioRerio.PhyloMap <- DanioRerioPhyloMap.BMCGenomics[ , c(2,1)]

# have a look at the final format
head(DanioRerio.PhyloMap)
```

```
  Oldest Phylostratum    Ensembl Gene ID
1                   1 ENSDARG00000033231
2                   1 ENSDARG00000000102
3                   1 ENSDARG00000000241
4                   1 ENSDARG00000000370
5                   1 ENSDARG00000000380
6                   1 ENSDARG00000000472
```

### _Gasterosteus aculeatus_

```r

# read the excel file: Gasterosteus aculeatus
GasterosteusAculeatusPhyloMap.BMCGenomics <- read_excel("BMCGenomics_2013_species_PhyloMaps.xlsx", sheet = 4)

# format Phylostratigraphic Map of Gasterosteus aculeatus for use with myTAI
GasterosteusAculeatus.PhyloMap <- GasterosteusAculeatusPhyloMap.BMCGenomics[ , c(2,1)]

# have a look at the final format
head(GasterosteusAculeatus.PhyloMap)
```

```
  Oldest Phylostratum    Ensembl Gene ID
1                   1 ENSGACG00000000009
2                   1 ENSGACG00000000017
3                   1 ENSGACG00000000018
4                   1 ENSGACG00000000019
5                   1 ENSGACG00000000022
6                   1 ENSGACG00000000027
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Maps` of the aforementioned species from [Neme and Tautz, 2013](http://www.biomedcentral.com/1471-2164/14/117) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).



