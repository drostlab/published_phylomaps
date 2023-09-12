![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%HajkD%2Fpublished_phylomaps&label=VISITORS&countColor=%23263759&style=flat)


# General Overview

Gene Age Inference is the foundation of most [Evolutionary Transcriptomics](https://github.com/HajkD/myTAI#perform-evolutionary-transcriptomics-with-r) studies.
The concept behind Evolutionary Transcriptomics is to combine these gene age estimates with gene expression
data to quantify the average transcriptome age within a biological process of interest ([Drost et al., 2018, _Bioinformatics_](https://academic.oup.com/bioinformatics/article/34/9/1589/4772684)).

In particular, this approach allowed the quantification of transcriptome conservation of animal and plant embryos passing through embryogenesis by first individually estimating the gene ages of specific animal and plant genomes and combining these gene age estimates with transcriptome data covering several stages of embryo development ([Domazet-Loso and Tautz, 2010 _Nature_](http://www.nature.com/nature/journal/v468/n7325/full/nature09632.html) ; [Quint, Drost et al., 2012 _Nature_](http://www.nature.com/nature/journal/v490/n7418/full/nature11394.html) ; [Drost et al., 2015 _Mol. Biol. Evol._](http://mbe.oxfordjournals.org/content/32/5/1221) ; [Drost et al., 2016 _Mol. Biol. Evol._](http://mbe.oxfordjournals.org/content/early/2016/02/23/molbev.msw039.short?rss=1)).

However, as intensely discussed in the past years ([Capra et al., 2013](http://www.sciencedirect.com/science/article/pii/S016895251300111X); [Altenhoff et al., 2016](http://www.nature.com/nmeth/journal/v13/n5/pdf/nmeth.3830.pdf); [Liebeskind et al., 2016](http://gbe.oxfordjournals.org/content/early/2016/06/03/gbe.evw113)), gene age inference is not a trivial task and might be biased in some currently existing approaches ([Liebeskind et al., 2016](http://gbe.oxfordjournals.org/content/early/2016/06/03/gbe.evw113)).

In particular, Moyers & Zhang argue that [genomic phylostratigraphy](http://www.sciencedirect.com/science/article/pii/S0168952507002995) (a prominent BLAST based gene age inference method) 1) underestimates gene age for a considerable fraction of genes, 2) is biased for rapidly evolving proteins which are short, and/or their most conserved block of sites is small, and 3) these biases create spurious nonuniform distributions of various gene properties among age groups, many of which cannot be predicted a priori ([Moyers & Zhang, 2015](http://mbe.oxfordjournals.org/content/32/1/258.long);  [Moyers & Zhang, 2016](http://mbe.oxfordjournals.org/content/33/5/1245); [Liebeskind et al., 2016](http://gbe.oxfordjournals.org/content/early/2016/06/03/gbe.evw113)). However, these arguments were based on simulated data and were inconclusive due to [errors in their analyses](http://mbe.oxfordjournals.org/content/33/11/3031.full?etoc). Furthermore, [Domazet-Loso et al., 2016](http://www.biorxiv.org/content/early/2016/06/26/060756.abstract) provide convincing evidence that there is __no__ phylostratigraphic bias. In general, however, an objective benchmarking set representing the tree of life is still missing and therefore any procedure aiming to quantify gene ages will be biased to some degree.

Based on this debate [Liebeskind et al., 2016](http://gbe.oxfordjournals.org/content/early/2016/06/03/gbe.evw113) suggest to perform gene age inference by combining thirteen common orthology inference algorithms to create gene age datasets and then characterize the error around each age-call on a per-gene and per-algorithm basis. Using this approach systematic error was found to be a large factor in estimating gene age, suggesting that simple consensus algorithms are not enough to give a reliable point estimate. However, by generating a consensus gene age and quantifying the possible error in each workflow step, [Liebeskind et al., 2016](http://gbe.oxfordjournals.org/content/early/2016/06/03/gbe.evw113) provide a very useful [database](http://geneages.org/) of consensus gene ages for a variety of genomes. 

Alternatively, [Stephen Smith, 2016](https://bib.oxfordjournals.org/content/early/2016/04/20/bib.bbw034.full) argues that _de novo_ gene birth/death and gene family expansion/contraction studies should avoid drawing direct inferences of evolutionary relatedness from measures of sequence similarity alone, and should instead, where possible, use more rigorous phylogeny-based methods. For this purpose, I recommend researchers to consult the [phylomedb database](http://orthology.phylomedb.org/) to retrieve phylogeny-based gene orthology relationships and use these age estimates in combination with [myTAI](https://github.com/HajkD/myTAI).

In addition, [Weisman et al., 2020](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.3000862) test and discuss the issue of _homology detection failure_, i.e., the inability of pairwise local aligners to trace back distantly related homologs only due to neutral sequence divergence which results in spurious patterns of TRG birth (as also discussed in [Barrera-Redondo et al., 2023](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-023-02895-z)). Homology detection failure can cause especially small and fast-evolving genes to be wrongly annotated as young genes.

A recent publication by [Barrera-Redondo et al., 2023](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-023-02895-z) has sought to overcome this limitation and increase the speed and scalability of gene age inference using [`DIAMOND`](https://github.com/bbuchfink/diamond) instead of blast for local pairwise sequence alignment. The effects of horizontal gene transfer and database contaminations are also mitigated with the taxonomic representativeness thresholds. Furthermore, [Barrera-Redondo et al., 2023](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-023-02895-z) have examined the effect of other alignment approaches such as protein _structure_ alignment for gene age inference.

The [myTAI](https://github.com/HajkD/myTAI) package aims to provide a standard tool for Evolutionary Transcriptomics studies and relies
on gene age estimate tables as input. Hence, I recommend to follow the active discussion on gene age inference and to consult all available resources to robustly estimate gene age (for ex. use the consensus gene age estimates provided by 
[Liebeskind et al., 2016](http://gbe.oxfordjournals.org/content/early/2016/06/03/gbe.evw113) and _phylostratigraphic maps_ generated by phylostratigraphy to quantify transcriptome age with `myTAI`).

In case researchers would like to perform _genomic phylostratigraphy_, [GenEra](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-023-02895-z) has recently been released and can be used to generate high quality phylostratigraphic maps. Instructions for using `GenEra` is provided [here](https://github.com/josuebarrera/GenEra).
Previous tools for _genomic phylostratigraphy_ include [ORFanFinder](http://bioinformatics.oxfordjournals.org/content/early/2016/03/26/bioinformatics.btw122).

Evidently, these advancements in gene age research are very recent and gene age inference is a very young and active field of genomic research. Therefore, many more studies need to address the robust and realistic inference
of gene age and a community standard is still missing.

To provide a comprehensive resource of gene ages, I accumulated all phylostratigraphic maps or sequence divergence maps that have been published to date and they might nevertheless be useful to study global patterns of transcriptome conservation in biological processes.

However, future Evolutionary Transcriptomics studies (this will include my own research) should consider these new advancements in gene age inference methods and concepts, because they will allow researchers to quantify transcriptome conservation or estimate the average transcriptome age with [myTAI](https://github.com/HajkD/myTAI) more accurately and more robustly. 


__If your study recently published a phylostratigraphic map or sequence divergence map, please contact me (https://github.com/HajkD/published_phylomaps/issues) and I will gladly reference you and include your study in the following list.__

## A Collection of Published Phylostratigraphic Maps and Divergence Maps

The following studies include published `Phylostratigraphic Maps` and `Divergence Maps` based on similar approaches, but using different parameter sets.
This collection aims to store all published maps and furthermore, provides scripts for easy data retrieval to be able to integrate corresponding maps into a phylostranscriptomics workflow with [myTAI](https://github.com/HajkD/myTAI).

The [Introduction to Phylotranscriptomics](https://drostlab.github.io/myTAI/articles/Introduction.html) Vignette introduces the integration of the following `Phylostratigraphic Maps` and `Divergence Maps` to perform custom phylotranscriptomic analyses.

__Note: some of the phylostratigraphic maps are now retrievable via the R data package, [`phylomapr`](https://github.com/LotharukpongJS/phylomapr). More will be added in the near future.__

## Table of Contents
**Animals**
- _Homo sapiens_
  - [Tomislav Domazet-Lošo and Diethard Tautz, 2008](#tomislav-domazet-lošo-and-diethard-tautz-2008)
  - [Tomislav Domazet-Lošo and Diethard Tautz, 2010](#tomislav-domazet-lošo-and-diethard-tautz-2010)
  - [Rafik Neme and Diethard Tautz, 2013](#rafik-neme-and-diethard-tautz-2013)
  - [Jaruwatana Sodai Lotharukpong (unpublished)](#)
- _Drosophila melanogaster_
  - [Martin Sebastijan Šestak and Tomislav Domazet-Lošo, 2015](#martin-sebastijan-šestak-and-tomislav-domazet-lošo-2015)
  - [Hajk-Georg Drost, Alexander Gabel, Ivo Grosse, Marcel Quint, 2015](#hajk-georg-drost-alexander-gabel-ivo-grosse-marcel-quint-2015)
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Danio rerio_
  - [Rafik Neme and Diethard Tautz, 2013](#rafik-neme-and-diethard-tautz-2013)
  - [Martin Sebastijan Šestak and Tomislav Domazet-Lošo, 2015](#martin-sebastijan-šestak-and-tomislav-domazet-lošo-2015)
  - [Hajk-Georg Drost, Alexander Gabel, Ivo Grosse, Marcel Quint, 2015](#hajk-georg-drost-alexander-gabel-ivo-grosse-marcel-quint-2015)
- _Mus musculus_ (mouse)
  - [Rafik Neme and Diethard Tautz, 2013](#rafik-neme-and-diethard-tautz-2013)
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Gasterosteus aculeatus_ (three-spined stickleback)
  - [Rafik Neme and Diethard Tautz, 2013](#rafik-neme-and-diethard-tautz-2013)
- _Crassostrea gigas_ (Pacific oyster)
  - [Xu F, Domazet-Lošo T, Fan D, Dunwell TL, Li L, Fang X, Zhang G., 2016](#xu-f-domazet-lošo-t-fan-d-dunwell-tl-li-l-fang-x-zhang-g-2016)
- _Haliotis discus_ (Pacific abalone)
  - [Xu F, Domazet-Lošo T, Fan D, Dunwell TL, Li L, Fang X, Zhang G., 2016](#xu-f-domazet-lošo-t-fan-d-dunwell-tl-li-l-fang-x-zhang-g-2016)
- _Perinereis aibuhitensis_ (sand worm)
  - [Xu F, Domazet-Lošo T, Fan D, Dunwell TL, Li L, Fang X, Zhang G., 2016](#xu-f-domazet-lošo-t-fan-d-dunwell-tl-li-l-fang-x-zhang-g-2016)
- _Caenorhabditis elegans_
  - [Shuai Sun, Christian Roedelsperger & Ralf J. Sommer, 2021](#shuai-sun-christian-roedelsperger--ralf-j-sommer-2021)
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Pristionchus pacificus_
  - [Shuai Sun, Christian Roedelsperger & Ralf J. Sommer, 2021](#shuai-sun-christian-roedelsperger--ralf-j-sommer-2021)
- _Echinococcus granulosus_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Octopus vulgaris_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Capitella teleta_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Apostichopus japonicus_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Nematostella vectensis_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Trichoplax adhaerens_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Amphimedon queenslandica_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)

**Plants**
- _Arabidopsis thaliana_
  - [Marcel Quint, Hajk-Georg Drost, Alexander Gabel, Kristian Karsten Ullrich, Markus Boenn, Ivo Grosse, 2012](#marcel-quint-hajk-georg-drost-alexander-gabel-kristian-karsten-ullrichmarkus-boenn-ivo-grosse-2012)
  - [Hajk-Georg Drost, Alexander Gabel, Ivo Grosse, Marcel Quint, 2015](#hajk-georg-drost-alexander-gabel-ivo-grosse-marcel-quint-2015)
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Glycine max_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Solanum lycopersicum_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Oryza sativa_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Vanilla planifolia_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Musa acuminata_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Picea glauca_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Selaginella moellendorffii_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Physcomitrella patens_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Marchantia polymorpha_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)

**Fungi**
- _Coprinopsis cinerea_ (gray shag)
  - [Xuanjin Cheng, Jerome Ho Lam Hui, Yung Yung Lee, Patrick Tik Wan Law and Hoi Shan Kwan, 2015](#xuanjin-cheng-jerome-ho-lam-hui-yung-yung-lee-patrick-tik-wan-law-and-hoi-shan-kwan-2015)
- _Saccharomyces cerevisiae_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Schizosaccharomyces pombe_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Aspergillus niger_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Morchella conica_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Cryptococcus neoformans_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Kwoniella mangroviensis_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Agaricus bisporus_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Tremella mesenterica_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Mucor circinelloides_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Batrachochytrium dendrobatidis_
  - [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](#josué-barrera-redondo-jaruwatana-sodai-lotharukpong-hajk-georg-drost--susana-m-coelho-2023)
- _Rhizophagus irregularis_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)
- _Geosiphon pyriformis_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)
- _Gigaspora margarita_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)
- _Dissophora decumbens_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)
- _Mortierella elongata_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)
- _Radiomyces spectabilis_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)
- _Phycomyces blakesleeanus_
  - [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](#bethan-f-manley-jaruwatana-s-lotharukpong-josué-barrera-redondo-theo-llewellyn-gokalp-yildirir-jana-sperschneider-nicolas-corradi-uta-paszkowski-eric-a-miska-alexandra-dallaire-2023)

## [Tomislav Domazet-Lošo, Josip Brajković, Diethard Tautz, 2007](http://www.sciencedirect.com/science/article/pii/S0168952507002995)

__Title__: _A phylostratigraphy approach to uncover the genomic history of major adaptations in metazoan lineages_

This study introduced `Phylostratigraphy` as computational method to quantify gene age in terms of sequence homology resulting in an organism specific `Phylostratigraphic Map`.

Published `Phylostratigraphic Map`:

- __Organisms__: _Drosophila melanogaster_ (fly)
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)

__Data sets are not available as Supplementary Tables.__


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
download.file( url      = "https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/mbe/25/12/10.1093_molbev_msn214/2/msn214_Supplementary_Data.zip?Expires=1690187066&Signature=UprdKTMgmqkhITKxIxbE74~blDUfhi2rgQn57X5d3YfFEM-bMqqC~LqMLJjGjlNkwOBrR2XGgOwWPyh4UEkXBdcpTbHiH71YFyZUeMJHhVBCLJQ7ceztyOJyrQC8sVScYyUZuPtOtgLgjdMrk5eP72P4R~pj-mPaIxx43efDP4VhjebsYjx8ICB~VEGZRMFAdfpKn8OZyLnMOuE37W3lRwpF9Nyr3~Tk7DUaIGmtzY6mv6mCmcO6bo2aq3pdXWkenDCo2rW-Mtdr8SN3fyClJZjFNHOMYFj4fgRjQoLUCSn-5JH59xqEvETalQTCdqV4y5h280AGrEcPp8CFfQwNhg__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA",
               destfile = "MBE_2008_Homo_Sapiens_PhyloMap.zip")

utils::unzip( zipfile = "MBE_2008_Homo_Sapiens_PhyloMap.zip",
              files = "mbe-08-0522-File008_msn214.xls")

HomoSapiensPhyloMap.MBE <- read_excel("mbe-08-0522-File008_msn214.xls", sheet = 1, skip = 1)

    
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
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1186%2F1741-7007-8-66/MediaObjects/12915_2009_362_MOESM1_ESM.xls", 
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
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1038%2Fnature11394/MediaObjects/41586_2012_BFnature11394_MOESM335_ESM.xls", 
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
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1038%2Fnature11394/MediaObjects/41586_2012_BFnature11394_MOESM336_ESM.xls", 
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
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1186%2F1471-2164-14-117/MediaObjects/12864_2012_4867_MOESM1_ESM.xlsx", 
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

## [Martin Sebastijan Šestak and Tomislav Domazet-Lošo, 2015](http://mbe.oxfordjournals.org/content/32/2/299.short)

__Title__: _Phylostratigraphic Profiles in Zebrafish Uncover Chordate Origins of the Vertebrate Brain_

Published `Phylostratigraphic Map`:

- __Organisms__: _Danio rerio_ (zebrafish) and _Drosophila melanogaster_
- __E-value cutoff__: 1E-3 (blastp; protein sequences) and 1E-15 (tblastn; ESTs) 
- __Sequence type__: Protein Sequences and ESTs
- __Reference data bases__: NCBI nr (protein); trace and EST archives (EST)
- __Splice variants__: always using the longest splice variant


Download Map using R:

```r
# download the Phylostratigraphic Map of Danio rerio
# from Šestak and Domazet-Lošo, 2015

download.file( url      = "https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/mbe/32/2/10.1093_molbev_msu319/1/msu319_Supplementary_Data.zip?Expires=1690187793&Signature=IaT8wOG0Q2ftMybR2s2JaQu0z38sToxHW4p7HZ3XFNBC089SoMLBkxhLzpvp9nHypm14pM4RLJZXxX5zi~m9Zl29tlIXHgzu75zVddtgP6qDDZ4m00~JTCRIiivLTzmNlAjthM5hzvDkAPuy8j8Ya0KLUVRy0867nVRsY58weDf1Ql79ZiWNT1TTIXMGD~l2OPT4kSTaCOtiZ6xyIceXwDCo~6dgA82MC1LuFdNUXkaEPJ7NhtDHvpQ1CqF474TfIqpBZ~TCGv0Q1hhbDA~q0o-TMsPvsOIueHpnrvPj6nEPlHJDC0G2mdbE7si5gjFi5T7Ll5Ctw-l3a5zyeuWEdw__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA",
               destfile = "MBE_2015a_Drerio_PhyloMap.zip")

utils::unzip( zipfile = "MBE_2015a_Drerio_PhyloMap.zip",
              files = "TableS3-2.xlsx")
               
# download the Phylostratigraphic Map of Drosophila melanogaster
# from Šestak and Domazet-Lošo, 2015
utils::unzip( zipfile = "MBE_2015a_Drerio_PhyloMap.zip",
              files = "TableS6.xlsx")
    
```

Read the `*.xlsx` file storing the `Phylostratigraphic Map` of _D. rerio_ and _D. melanogaster_ and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
DrerioPhyloMap.MBEa <- read_excel("TableS3-2.xlsx", sheet = 1, skip = 4)

# format Phylostratigraphic Map for use with myTAI
Drerio.PhyloMap <- DrerioPhyloMap.MBEa[ , 1:2]

# have a look at the final format
head(Drerio.PhyloMap)
```

```
  Phylostrata            ZFIN_ID
1           1 ZDB-GENE-000208-13
2           1 ZDB-GENE-000208-17
3           1 ZDB-GENE-000208-18
4           1 ZDB-GENE-000208-23
5           1  ZDB-GENE-000209-3
6           1  ZDB-GENE-000209-4
```

```r
# read the excel file
DmelanogasterPhyloMap.MBEa <- read_excel("TableS6.xlsx", sheet = 1, skip = 4)

# format Phylostratigraphic Map for use with myTAI
Dmelanogaster.PhyloMap <- DmelanogasterPhyloMap.MBEa[ , 1:2]

# have a look at the final format
head(Dmelanogaster.PhyloMap)
```

```
  Phylostrata FlyBase_Gene_ID
1           1     FBgn0000017
2           1     FBgn0000024
3           1     FBgn0000032
4           1     FBgn0000036
5           1     FBgn0000038
6           1     FBgn0000039
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Maps` of the aforementioned species from [Šestak and Domazet-Lošo, 2015](http://mbe.oxfordjournals.org/content/32/2/299.short) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).


## [Hajk-Georg Drost, Alexander Gabel, Ivo Grosse, Marcel Quint, 2015](http://mbe.oxfordjournals.org/content/32/5/1221.short?rss=1)

__Title__: _Evidence for Active Maintenance of Phylotranscriptomic Hourglass Patterns in Animal and Plant Embryogenesis_

Published `Phylostratigraphic Map`:

- __Organisms__: _Danio rerio_ (zebrafish), _Drosophila melanogaster_ (fly), and _Arabidopsis thaliana_
- __E-value cutoff__: 1E-5 (blastp; protein sequences)
- __Sequence type__: Protein Sequences
- __Reference data bases__: NCBI nr (protein) + custom selection of genomes (phytozome, flybase)
- __Splice variants__: always using the longest splice variant

Published `Divergence Maps`:

- __Organisms__: _Arabidopsis thaliana_ versus _Arabidopsis lyrata_; _Arabidopsis thaliana_ versus _Brassica rapa_; _Arabidopsis thaliana_ versus _Capsella rubella_; _Arabidopsis thaliana_ versus _Thelungiella halophila_; _Danio rerio_ versus _A. mexicanus_ ; _Danio rerio_ versus _F. rubripes_; _Danio rerio_ versus _X. maculatus_ ; _Danio rerio_ versus _G. morhua_ ; _Drosophila melanogaster_ versus _D. simulans_ ; _Drosophila melanogaster_ versus _D. yakuba_ ; _Drosophila melanogaster_ versus _D. persimilis_ ; _Drosophila melanogaster_ versus _D. virilis_ ;
- __E-value cutoff__: 1E-5 (blastp - best reciprocal hit; protein sequences) 
- __Sequence type__: CDS + Protein Sequences

Download Maps using R:

```r
# download the Phylostratigraphic Maps
# from Drost et al., 2015
download.file( url      = "http://files.figshare.com/1798295/Supplementary_table_S2.xls", 
               destfile = "MBE_2015b_PhyloMaps.xls" )
               
               
# download the Divergence Maps
download.file( url      = "http://files.figshare.com/1798297/Supplementary_table_S4.xls", 
               destfile = "MBE_2015b_DivergenceMaps.xls" )
    
```

Read the `*.xls` file storing the `Phylostratigraphic Maps` and `Divergence Maps` and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
DrerioPhyloMap.MBEb <- read_excel("MBE_2015b_PhyloMaps.xls", sheet = 1)

# have a look at the final format
head(DrerioPhyloMap.MBEb)
```

```
  Phylostratum             GeneID
1            1 ENSDARG00000000002
2            1 ENSDARG00000000019
3            1 ENSDARG00000000102
4            1 ENSDARG00000000241
5            1 ENSDARG00000000324
6            1 ENSDARG00000000369
```

```r
# load package readxl
library(readxl)

# read the excel file
DmelanogasterPhyloMap.MBEb <- read_excel("MBE_2015b_PhyloMaps.xls", sheet = 2)

# have a look at the final format
head(DmelanogasterPhyloMap.MBEb)
```

```
  Phylostratum      GeneID
1            1 fbpp0070006
2            1 fbpp0070025
3            1 fbpp0070051
4            1 fbpp0070054
5            1 fbpp0070061
6            1 fbpp0070064
```

```r
# load package readxl
library(readxl)

# read the excel file
Athaliana.MBEb <- read_excel("MBE_2015b_PhyloMaps.xls", sheet = 3)

# have a look at the final format
head(Athaliana.MBEb)
```

```
  Phylostratum      GeneID
1            1 at1g01040.2
2            1 at1g01050.1
3            1 at1g01070.1
4            1 at1g01080.2
5            1 at1g01090.1
6            1 at1g01120.1
```

```r
# load package readxl
library(readxl)

# Danio rerio

# D. rerio vs. A. mexicanus
Drerio_vs_Amex_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 9)
# D. rerio vs. F. rubripes
Drerio_vs_Frubripes_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 10)
# D. rerio vs. X. maculatus
Drerio_vs_Xmac_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 11)
# D. rerio vs. G. morhua
Drerio_vs_Gmor_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 12)



# Drosophila melanogaster

# D. melanogaster vs. D. simulans
Dmel_Dsim_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 1)
# D. melanogaster vs. D. yakuba
Dmel_Dyak_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 2)
# D. melanogaster vs. D. persimilis
Dmel_Dper_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 3)
# D. melanogaster vs. D. virilis
Dmel_Dvir_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 4)



# Arabidopsis thaliana

# A. thaliana vs A. lyrata
Ath_Aly_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 5)
# A thaliana vs. T. halophila
Ath_Brapa_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 8)
# A thaliana vs. C. rubella
Ath_Crub_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 7)
# A thaliana vs. C. papaya 
Ath_Cpapaya_DivergenceExpressionSet <- read_excel("MBE_2015b_DivergenceMaps.xls",sheet = 6)

```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Maps` and `Divergence Maps` of the aforementioned species from [Drost et al., 2015](http://mbe.oxfordjournals.org/content/32/5/1221.short?rss=1) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).


## [Xuanjin Cheng, Jerome Ho Lam Hui, Yung Yung Lee, Patrick Tik Wan Law and Hoi Shan Kwan, 2015](http://mbe.oxfordjournals.org/content/early/2015/05/08/molbev.msv047)

__Title__: _A “Developmental Hourglass” in Fungi_

Published `Phylostratigraphic Map`:

- __Organisms__: _Coprinopsis cinerea_ (fungi)
- __E-value cutoff__: 1E-3 (blastp; protein sequences)
- __Sequence type__: Protein Sequences
- __Reference data bases__: NCBI nr (protein) + custom selection of genomes
- __Splice variants__: always using the longest splice variant

Download `Phylostratigraphic Map` and `KaKsMaps` in R:

```r
# download the Phylostratigraphic Map of Coprinopsis cinerea
# from Cheng et al., 2015
download.file( url      = "https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/mbe/32/6/10.1093_molbev_msv047/2/msv047_Supplementary_Data.zip?Expires=1690186915&Signature=ZU-Sy0xAdxdvcnmoJuoCH9vX95C5~6gQxN9IJ-jhlmAeVkN9Lmil1NBgOGL2q42uNodckyT2w4B-8q2JfLQP1HJ5~GnxMJAVbxbCMkoxnOsd6PIH-a8Y~PAUlLbVqAEEbroCsDBwzLd6dykBfDRhtX3xYYZCWc8UWqyk2mL0tFKVdaKYUGWtl9WlWb-BUcUrtYBJpmuh7OCj2POzt0YJ-a-fqoqx9Usq6KtvgV2RbdwSQb3mvavzio8a99yjBZBC0MPQOimwdWSoRdoIXC1Ey2NzTMDOqy-t1vEceVr4vK7t3laZOHUP8N43MXM5rFdmq6rbo3ggLOZJSFf9jpcM7A__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA", 
               destfile = "MBE_2015c_Ccinerea_Maps.zip" )

utils::unzip( zipfile = "MBE_2015c_Ccinerea_Maps.zip",
              files = "Table_S9.xlsx")
               
```

Read the `*.xls` file storing the `Phylostratigraphic Maps` and `Divergence Maps` and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# load package readxl
library(readxl)

# Coprinopsis cinerea Phylostratigraphic Map

CcinereaPhyloMap.MBEc <- read_excel("Table_S9.xlsx", sheet = 2)

Ccinerea.PhyloMap <- CcinereaPhyloMap.MBEc[ , c(4,1)]

colnames(Ccinerea.PhyloMap) <- c("Phylostratum", "GeneID")

# have a look at the final format
head(Ccinerea.PhyloMap)

```

```
  Phylostratum     GeneID
1           10 CC1G_00004
2            4 CC1G_00007
3            3 CC1G_00011
4            2 CC1G_00012
5            3 CC1G_00013
6            2 CC1G_00014

```

```r
# load package readxl
library(readxl)

# Coprinopsis cinerea KaKs Maps

CcinereaKaKsMaps.MBEc <- read_excel("Table_S9.xlsx", sheet = 3, skip = 1)

# Coprinopsis cinerea versus Agaricus bisporus var bisporus H97
Ccin_vs_Abisp.KaKsMap <- CcinereaKaKsMaps.MBEc[ , c(2,1)]

# Coprinopsis cinerea versus Laccaria bicolor
Ccin_vs_Lbicol.KaKsMap <- CcinereaKaKsMaps.MBEc[ , c(5,1)]

# Coprinopsis cinerea versus Lentinula edodes
Ccin_vs_Ledodes.KaKsMap <- CcinereaKaKsMaps.MBEc[ , c(8,1)]

# Coprinopsis cinerea versus Schizophyllum commune
Ccin_vs_Scommune.KaKsMap <- CcinereaKaKsMaps.MBEc[ , c(11,1)]

# have a look at the final format: example -> Ccin_vs_Abisp.KaKsMap
head(Ccin_vs_Abisp.KaKsMap)

```

```
                  dN/dS    Gene_id
1   0.20669999999999999 CC1G_00007
2 7.6300000000000007E-2 CC1G_00011
3   0.15290000000000001 CC1G_00012
4                0.3362 CC1G_00013
5                2.7E-2 CC1G_00014
6 3.5700000000000003E-2 CC1G_00015
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Maps` and `KaKs Maps` of the aforementioned species from [Cheng et al., 2015](http://mbe.oxfordjournals.org/content/early/2015/05/08/molbev.msv047) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).

## [Xu F, Domazet-Lošo T, Fan D, Dunwell TL, Li L, Fang X, Zhang G., 2016](http://www.nature.com/articles/srep34664)

__Title__: _High expression of new genes in trochophore enlightening the ontogeny and evolution of trochozoans_

Published `Phylostratigraphic Map`:

- __Organisms__: _oyster_, _abalone_, _sand worm_
- __E-value cutoff__: E-value cutoff is not specified in the paper (blastp searches were conducted against the database using oyster proteins, while blastx searches were conducted using the unigenes of abalones and sand worms)
- __Sequence type__: Protein Sequences, Unigenes
- __Reference data bases__: NCBI nr (protein) + custom selection of genomes
- __Splice variants__: Not specified in the paper

Download `Phylostratigraphic Maps` in R:

```r
# download the Phylostratigraphic Maps of oyster, abalone, sand worm
# from Xu et al., 2016
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1038%2Fsrep34664/MediaObjects/41598_2016_BFsrep34664_MOESM2_ESM.xls", 
               destfile = "Xu_2016_Maps.xls" )
               
```

Read the `*.xls` file storing the `Phylostratigraphic Maps` and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# load package readxl
library(readxl)

### Oyster1 Phylostratigraphic Map

oyster1.data <- read_excel("Xu_2016_Maps.xls", sheet = 1)

Oyster1.PhyloMap <- dplyr::select(oyster1.data, age, GeneID)

colnames(Oyster1.PhyloMap) <- c("Phylostratum", "GeneID")

# have a look at the final format
Oyster1.PhyloMap


### Oyster2 Phylostratigraphic Map
oyster2.data <- read_excel("Xu_2016_Maps.xls", sheet = 2)

Oyster2.PhyloMap <- dplyr::select(oyster2.data, age, GeneID)

colnames(Oyster2.PhyloMap) <- c("Phylostratum", "GeneID")

# have a look at the final format
Oyster2.PhyloMap


### Abalone Phylostratigraphic Map
abalone.data <- read_excel("Xu_2016_Maps.xls", sheet = 3)

Abalone.PhyloMap <- dplyr::select(abalone.data, age, UnigeneID)

colnames(Abalone.PhyloMap) <- c("Phylostratum", "GeneID")

# have a look at the final format
Abalone.PhyloMap


### Sand worm Phylostratigraphic Map
sandworm.data <- read_excel("Xu_2016_Maps.xls", sheet = 4)

Sandworm.PhyloMap <- dplyr::select(sandworm.data, age, UnigeneID)

colnames(Sandworm.PhyloMap) <- c("Phylostratum", "GeneID")

# have a look at the final format
Sandworm.PhyloMap
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Maps`  of the aforementioned species from [Xu et al., 2016](http://www.nature.com/articles/srep34664) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).

## [Shuai Sun, Christian Roedelsperger & Ralf J. Sommer, 2021](https://genome.cshlp.org/content/early/2021/07/22/gr.275303.121)

__Title__: _Single worm transcriptomics identifies a developmental core network of oscillating genes with deep conservation across nematodes_

Published `Phylostratigraphic Map`:

- __Organisms__: _Caenorhabditis elegans_, _Pristionchus pacificus_
- __E-value cutoff__: 1E-3 ([DIAMOND](https://github.com/bbuchfink/diamond); protein sequences)
- __Sequence type__: Protein Sequences
- __Reference data bases__: WormBase (protein)
- __Splice variants__: longest isoform

Download Maps using R:

```r
# download the Phylostratigraphic Maps
# from Sun et al., 2021
download.file( url      = "https://genome.cshlp.org/content/suppl/2021/08/23/gr.275303.121.DC1/Supplemental_Table_S5.xlsx", 
               destfile = "GenomeResearch_2021_PhyloMap_Pp.xlsx" )

download.file( url      = "https://genome.cshlp.org/content/suppl/2021/08/23/gr.275303.121.DC1/Supplemental_Table_S6.xlsx", 
               destfile = "GenomeResearch_2021_PhyloMap_Ce.xlsx" )

```

Read the `*.xls` file storing the `Phylostratigraphic Maps` and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# install the readxl package
install.packages("readxl")

# load package readxl
library(readxl)

# read the excel file
PpacificusPhyloMap <- read_excel("GenomeResearch_2021_PhyloMap_Pp.xlsx", sheet = 1, skip = 1)
colnames(PpacificusPhyloMap) <- c("GeneID", "Phylostratum")
PpacificusPhyloMap$Phylostratum <- gsub("unsign", "p00", PpacificusPhyloMap$Phylostratum)
PpacificusPhyloMap$Phylostratum <- as.numeric(gsub("p", "", PpacificusPhyloMap$Phylostratum))

# have a look at the final format
head(PpacificusPhyloMap)
```

```r
# load package readxl
library(readxl)

# read the excel file
CelegansPhyloMap <- read_excel("GenomeResearch_2021_PhyloMap_Ce.xlsx", sheet = 1, skip = 1)
colnames(CelegansPhyloMap) <- c("GeneID", "TranscriptID", "Phylostratum")
CelegansPhyloMap$Phylostratum <- gsub("unsign", "c00", CelegansPhyloMap$Phylostratum)
CelegansPhyloMap$Phylostratum <- as.numeric(gsub("c", "", CelegansPhyloMap$Phylostratum))

# have a look at the final format
head(CelegansPhyloMap)
```

Now you can use the `MatchMap()` function implemented in [myTAI](https://github.com/HajkD/myTAI) to match the `Phylostratigraphic Maps`  of the aforementioned species from [Sun et al., 2021](https://genome.cshlp.org/content/early/2021/07/22/gr.275303.121) to any gene expression set of your interest (see [Introduction to Phylotranscriptomics](https://github.com/HajkD/myTAI/blob/master/vignettes/Introduction.Rmd) for details).

## [Josué Barrera-Redondo, Jaruwatana Sodai Lotharukpong, Hajk-Georg Drost & Susana M. Coelho, 2023](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-023-02895-z)

__Title__: _Uncovering gene-family founder events during major evolutionary transitions in animals, plants and fungi using GenEra_

Published `Phylostratigraphic Map`:

- __Organisms__: 
  - Fungi: _Saccharomyces cerevisiae_ (strain S288C), _Schizosaccharomyces pombe_, _Aspergillus niger_ (strain CBS 513.88), _Morchella conica_, _Cryptococcus neoformans_ (var. neoformans strain JEC21), _Kwoniella mangroviensis_ (strain CBS 8507), _Agaricus bisporus_ (var. bisporus strain H97), _Tremella mesenterica_ (strain DSM 1558), _Mucor circinelloides_, _Batrachochytrium dendrobatidis_ (strain JAM81)
  - Animals: _Drosophila melanogaster_, _Caenorhabditis elegans_, _Echinococcus granulosus_, _Octopus vulgaris_, _Capitella teleta_,	_Mus musculus_,	_Apostichopus japonicus_, _Nematostella vectensis_,	_Trichoplax adhaerens_,	_Amphimedon queenslandica_
  - Plants: _Arabidopsis thaliana_, _Glycine max_, _Solanum lycopersicum_, _Oryza sativa_, _Vanilla planifolia_, _Musa acuminata_, _Picea glauca_, _Selaginella moellendorffii_, _Physcomitrella patens_, _Marchantia polymorpha_
- __E-value cutoff__: 1E-5 ([DIAMOND](https://github.com/bbuchfink/diamond); protein sequences; ultra-sensitive mode)
- __Sequence type__: Protein Sequences
- __Reference data bases__: NCBI nr (protein)
- __Splice variants__: always using the representative sequences from UniProt (under "Download one protein sequence per gene (FASTA)")

This study used [GenEra](https://github.com/josuebarrera/GenEra) for gene age inference (phylostratigraphy). The following NCBI Taxonomic-ID were used.

```
# Fungi
559292	Saccharomyces cerevisiae S288C
4896	Schizosaccharomyces pombe
425011	Aspergillus niger CBS 513.88
5194	Morchella conica
214684	Cryptococcus neoformans var. neoformans JEC21
1296122	Kwoniella mangroviensis CBS 8507
936046	Agaricus bisporus var. bisporus H97
578456	Tremella mesenterica DSM 1558
36080	Mucor circinelloides
684364	Batrachochytrium dendrobatidis JAM81
# Animals
7227	Drosophila melanogaster
6239	Caenorhabditis elegans
6210	Echinococcus granulosus
6645	Octopus vulgaris
283909	Capitella teleta
10090	Mus musculus
307972	Apostichopus japonicus
45351	Nematostella vectensis
10228	Trichoplax adhaerens
400682	Amphimedon queenslandica
# Plants
3702	Arabidopsis thaliana
3847	Glycine max
4081	Solanum lycopersicum
39947	Oryza sativa
51239	Vanilla planifolia
214687	Musa acuminata
3330	Picea glauca
88036	Selaginella moellendorffii
3218	Physcomitrella patens
3197	Marchantia polymorpha
```

Download `Phylostratigraphic Maps` in R:

```r
# download the Phylostratigraphic Maps of 10 animals, 10 plants and/or 10 fungi.
# [Fungus] from Barrera-Redondo et al., 2023
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1186%2Fs13059-023-02895-z/MediaObjects/13059_2023_2895_MOESM3_ESM.xlsx", 
               destfile = "Barrera-Redondo_2023_Maps_fungus.xlsx" )

# [Animals] from Barrera-Redondo et al., 2023
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1186%2Fs13059-023-02895-z/MediaObjects/13059_2023_2895_MOESM4_ESM.xlsx", 
               destfile = "Barrera-Redondo_2023_Maps_animal.xlsx" )

# [Plants] from Barrera-Redondo et al., 2023
download.file( url      = "https://static-content.springer.com/esm/art%3A10.1186%2Fs13059-023-02895-z/MediaObjects/13059_2023_2895_MOESM5_ESM.xlsx", 
               destfile = "Barrera-Redondo_2023_Maps_plant.xlsx" )
```

Read the `*.xlsx` file storing the `Phylostratigraphic Maps` and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# load package readxl
library(readxl)
library(dplyr)

### Fungus Phylostratigraphic Maps

# Budding yeast
Saccharomyces_cerevisiae_S288C.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "559292_gene_ages")
Saccharomyces_cerevisiae_S288C.PhyloMap <- 
  dplyr::select(
    Saccharomyces_cerevisiae_S288C.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Fission yeast
Schizosaccharomyces_pombe.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "4896_gene_ages")
Schizosaccharomyces_pombe.PhyloMap <- 
  dplyr::select(
    Schizosaccharomyces_pombe.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Black mould fungus
Aspergillus_niger_CBS_513.88.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "425011_gene_ages")
Aspergillus_niger_CBS_513.88.PhyloMap <- 
  dplyr::select(
    Aspergillus_niger_CBS_513.88.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Black morels
Morchella_conica.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "5194_gene_ages")
Morchella_conica.PhyloMap <- 
  dplyr::select(
    Morchella_conica.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Cryptococcus neoformans
Cryptococcus_neoformans_var.neoformans_JEC21.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "214684_gene_ages")
Cryptococcus_neoformans_var.neoformans_JEC21.PhyloMap <- 
  dplyr::select(
    Cryptococcus_neoformans_var.neoformans_JEC21.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Kwoniella mangroviensis (or K. mangrovensis)
Kwoniella_mangroviensis.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "1296122_gene_ages")
Kwoniella_mangroviensis.PhyloMap <- 
  dplyr::select(
    Kwoniella_mangroviensis.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Portobello mushrooms
Agaricus_bisporus.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "936046_gene_ages")
Agaricus_bisporus.PhyloMap <- 
  dplyr::select(
    Agaricus_bisporus.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Yellow brain (or goldeb jelly fungus, yellow trembler, witches' butter)
Tremella_mesenterica.data <- 
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "578456_gene_ages")
Tremella_mesenterica.PhyloMap <- 
  dplyr::select(
    Tremella_mesenterica.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Mucor circinelloides
Mucor_circinelloides.data <-
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "36080_gene_ages")
Mucor_circinelloides.PhyloMap <- 
  dplyr::select(
    Mucor_circinelloides.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Amphibian chytrid fungus
Batrachochytrium_dendrobatidis_JAM81.data <-
  read_excel("Barrera-Redondo_2023_Maps_fungus.xlsx", sheet = "684364_gene_ages")
Batrachochytrium_dendrobatidis_JAM81.PhyloMap <- 
  dplyr::select(
    Batrachochytrium_dendrobatidis_JAM81.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

### Animal Phylostratigraphic Maps

# Fruit fly
Drosophila_melanogaster.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "7227_gene_ages")
Drosophila_melanogaster.PhyloMap <- 
  dplyr::select(
    Drosophila_melanogaster.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Caenorhabditis elegans
Caenorhabditis_elegans.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "6239_gene_ages")
Caenorhabditis_elegans.PhyloMap <- 
  dplyr::select(
    Caenorhabditis_elegans.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Hydatid worm
Echinococcus_granulosus.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "6210_gene_ages")
Echinococcus_granulosus.PhyloMap <- 
  dplyr::select(
    Echinococcus_granulosus.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Common octopus
Octopus_vulgaris.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "6645_gene_ages")
Octopus_vulgaris.PhyloMap <- 
  dplyr::select(
    Octopus_vulgaris.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Capitella teleta
Capitella_teleta.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "283909_gene_ages")
Capitella_teleta.PhyloMap <- 
  dplyr::select(
    Capitella_teleta.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

#	House mouse
Mus_musculus.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "10090_gene_ages")
Mus_musculus.PhyloMap <- 
  dplyr::select(
    Mus_musculus.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

#	Japanese sea cucumber
Apostichopus_japonicus.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "307972_gene_ages")
Apostichopus_japonicus.PhyloMap <- 
  dplyr::select(
    Apostichopus_japonicus.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

#	Starlet sea anemone
Nematostella_vectensis.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "45351_gene_ages")
Nematostella_vectensis.PhyloMap <- 
  dplyr::select(
    Nematostella_vectensis.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Trichoplax adhaerens
Trichoplax_adhaerens.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "10228_gene_ages")
Trichoplax_adhaerens.PhyloMap <- 
  dplyr::select(
    Trichoplax_adhaerens.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Amphimedon queenslandica
Amphimedon_queenslandica.data <- 
  read_excel("Barrera-Redondo_2023_Maps_animal.xlsx", sheet = "400682_gene_ages")
Amphimedon_queenslandica.PhyloMap <- 
  dplyr::select(
    Amphimedon_queenslandica.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

### Plant Phylostratigraphic Maps

# Thale cress
Arabidopsis_thaliana.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "3702_gene_ages")
Arabidopsis_thaliana.PhyloMap <- 
  dplyr::select(
    Arabidopsis_thaliana.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Soybean
Glycine_max.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "3847_gene_ages")
Glycine_max.PhyloMap <- 
  dplyr::select(
    Glycine_max.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Tomato
Solanum_lycopersicum.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "4081_gene_ages")
Solanum_lycopersicum.PhyloMap <- 
  dplyr::select(
    Solanum_lycopersicum.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Rice
Oryza_sativa.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "39947_gene_ages")
Oryza_sativa.PhyloMap <- 
  dplyr::select(
    Oryza_sativa.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Flat-leaved vanilla
Vanilla_planifolia.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "51239_gene_ages")
Vanilla_planifolia.PhyloMap <- 
  dplyr::select(
    Vanilla_planifolia.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Musa acuminata
Musa_acuminata.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "214687_gene_ages")
Musa_acuminata.PhyloMap <- 
  dplyr::select(
    Musa_acuminata.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# White spruce
Picea_glauca.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "3330_gene_ages")
Picea_glauca.PhyloMap <- 
  dplyr::select(
    Picea_glauca.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Selaginella moellendorffii
Selaginella_moellendorffii.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "88036_gene_ages")
Selaginella_moellendorffii.PhyloMap <- 
  dplyr::select(
    Selaginella_moellendorffii.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Spreading earthmoss
Physcomitrella_patens.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "3218_gene_ages")
Physcomitrella_patens.PhyloMap <- 
  dplyr::select(
    Physcomitrella_patens.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))

# Marchantia polymorpha
Marchantia_polymorpha.data <- 
  read_excel("Barrera-Redondo_2023_Maps_plant.xlsx", sheet = "3197_gene_ages")
Marchantia_polymorpha.PhyloMap <- 
  dplyr::select(
    Marchantia_polymorpha.data,
    Phylostratum = rank,
    GeneID = `#gene`
  ) %>%
  dplyr::mutate(Phylostratum = as.numeric(Phylostratum))
```

## [Bethan F Manley, Jaruwatana S Lotharukpong, Josué Barrera-Redondo, Theo Llewellyn, Gokalp Yildirir, Jana Sperschneider, Nicolas Corradi, Uta Paszkowski, Eric A Miska, Alexandra Dallaire, 2023](https://academic.oup.com/g3journal/article/13/6/jkad077/7097621)

__Title__: _A highly contiguous genome assembly reveals sources of genomic novelty in the symbiotic fungus Rhizophagus irregularis_

Published `Phylostratigraphic Map`:

- __Organisms__: _Rhizophagus irregularis_, _Geosiphon pyriformis_, _Gigaspora margarita_, _Dissophora decumbens_, _Mortierella elongata_, _Radiomyces spectabilis_, _Phycomyces blakesleeanus_
- __E-value cutoff__: 1E-5 ([DIAMOND](https://github.com/bbuchfink/diamond); protein sequences; ultra-sensitive mode)
- __Sequence type__: Protein Sequences
- __Reference data bases__: NCBI nr (protein)
- __Splice variants__: always using the longest isoform when available

This study used [GenEra](https://github.com/josuebarrera/GenEra) for gene age inference (phylostratigraphy). The following NCBI Taxonomic-ID were used.

```
50956	Geosiphon pyriformis
4874	Gigaspora margarita
1432141	Rhizophagus irregularis
101101	Dissophora decumbens
1314771	Mortierella elongata
64574	Radiomyces spectabilis
4837 Phycomyces blakesleeanus
```

Download `Phylostratigraphic Maps` in R:

```r
# download the Phylostratigraphic Maps from Manley et al., 2023
# Rhizophagus irregularis
download.file( url      = "https://zenodo.org/record/7713976/files/Rhizophagus_irregularis_DAOM197198_1432141_phyloranks.tsv", 
               destfile = "Rhizophagus_irregularis_DAOM197198_1432141_phyloranks.tsv")
# Dissophora decumbens
download.file( url      = "https://zenodo.org/record/7713976/files/Disdec1_101101_phyloranks.tsv", 
               destfile = "Disdec1_101101_phyloranks.tsv")
# Geosiphon pyriformis
download.file( url      = "https://zenodo.org/record/7713976/files/Geopyr1_50956_phyloranks.tsv", 
               destfile = "Geopyr1_50956_phyloranks.tsv")
# Gigaspora margarita
download.file( url      = "https://zenodo.org/record/7713976/files/Gigmar1_4874_phyloranks.tsv", 
               destfile = "Gigmar1_4874_phyloranks.tsv")
# Mortierella elongata
download.file( url      = "https://zenodo.org/record/7713976/files/Morel2_1314771_phyloranks.tsv", 
               destfile = "Morel2_1314771_phyloranks.tsv")
# Phycomyces blakesleeanus
download.file( url      = "https://zenodo.org/record/7713976/files/Phybl2_4837_phyloranks.tsv", 
               destfile = "Phybl2_4837_phyloranks.tsv")
# Radiomyces spectabilis
download.file( url      = "https://zenodo.org/record/7713976/files/Radspe1_64574_phyloranks.tsv", 
               destfile = "Radspe1_64574_phyloranks.tsv")
```

Read the `*.tsv` file storing the `Phylostratigraphic Maps` and format it for the use with [myTAI](https://github.com/HajkD/myTAI):

```r
# load package readr
library(readr)

### Phylostratigraphic Maps
# Rhizophagus irregularis
Rhizophagus_irregularis.data <-readr::read_tsv("Rhizophagus_irregularis_DAOM197198_1432141_phyloranks.tsv")
Rhizophagus_irregularis.PhyloMap <- 
  dplyr::select(
    Rhizophagus_irregularis.data,
    Phylostratum = PS,
    GeneID
  )

# Dissophora decumbens
Dissophora_decumbens.data <-readr::read_tsv("Disdec1_101101_phyloranks.tsv")
Dissophora_decumbens.PhyloMap <- 
  dplyr::select(
    Dissophora_decumbens.data,
    Phylostratum = rank,
    GeneID = `#gene`
  )

# Geosiphon pyriformis
Geosiphon_pyriformis.data <-readr::read_tsv("Geopyr1_50956_phyloranks.tsv")
Geosiphon_pyriformis.PhyloMap <- 
  dplyr::select(
    Geosiphon_pyriformis.data,
    Phylostratum = rank,
    GeneID = `#gene`
  )

# Gigaspora margarita
Gigaspora_margarita.data <-readr::read_tsv("Gigmar1_4874_phyloranks.tsv")
Gigaspora_margarita.PhyloMap <- 
  dplyr::select(
    Gigaspora_margarita.data,
    Phylostratum = rank,
    GeneID = `#gene`
  )

# Mortierella elongata
Mortierella_elongata.data <-readr::read_tsv("Morel2_1314771_phyloranks.tsv")
Mortierella_elongata.PhyloMap <- 
  dplyr::select(
    Mortierella_elongata.data,
    Phylostratum = rank,
    GeneID = V1
  )

# Phycomyces blakesleeanus
Phycomyces_blakesleeanus.data <-readr::read_tsv("Phybl2_4837_phyloranks.tsv")
Phycomyces_blakesleeanus.PhyloMap <- 
  dplyr::select(
    Phycomyces_blakesleeanus.data,
    Phylostratum = rank,
    GeneID
  )

# Radiomyces spectabilis
Radiomyces_spectabilis.data <-readr::read_tsv("Radspe1_64574_phyloranks.tsv")
Radiomyces_spectabilis.PhyloMap <- 
  dplyr::select(
    Radiomyces_spectabilis.data,
    Phylostratum = rank,
    GeneID
  )
```

## [Jaruwatana S Lotharukpong (unpublished)](https://lotharukpongjs.github.io/phylomapr/reference/Homo_sapiens.PhyloMap.html)

Unpublished `Phylostratigraphic Map`:

- __Organisms__: _Homo sapiens_
- __E-value cutoff__: 1E-5 ([DIAMOND](https://github.com/bbuchfink/diamond); protein sequences; sensitive mode)
- __Sequence type__: Protein Sequences
- __Reference data bases__: NCBI nr (protein)
- __Splice variants__: always using the longest isoform when available

This study used [GenEra](https://github.com/josuebarrera/GenEra) for gene age inference (phylostratigraphy). NCBI Taxonomic-ID were used: 9606

```
9606	Homo sapiens
```

```r
# install phylomapr

devtools::install_github("LotharukpongJS/phylomapr")

# load package phylomapr
library(phylomapr)

### Phylostratigraphic Maps
# Homo sapiens
Homo_sapiens.PhyloMap <- phylomapr::Homo_sapiens.PhyloMap
```
