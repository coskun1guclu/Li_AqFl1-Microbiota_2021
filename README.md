<!-- badges: start -->
  [![DOI](https://zenodo.org/badge/272967155.svg)](https://zenodo.org/badge/latestdoi/272967155)
  [![Launch Rstudio Binder](http://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/yanxianl/Li_AqFl1-Microbiota_2020/master?urlpath=rstudio)
<!-- badges: end -->

## Consistent changes in the intestinal microbiota of Atlantic salmon fed insect meal diets (doi: https://doi.org/10.1186/s42523-021-00159-4)

### Abstract
**Background:** Being part of fish's natural diets, insects have become a practical alternative feed ingredient for aquaculture. While nutritional values of insects have been extensively studied in various fish species, their impact on the fish microbiota remains to be fully explored. In an 8-week freshwater feeding trial, Atlantic salmon (*Salmo salar*) were fed either a commercially relevant reference diet or an insect meal diet wherein black soldier fly (*Hermetia illucens*) larvae meal comprised 60% of total ingredients. Microbiota of digesta and mucosa origin from the proximal and distal intestine were collected and profiled along with feed and water samples. 

**Results:** The insect meal diet markedly modulated the salmon intestinal microbiota. Salmon fed the insect meal diet showed similar or lower alpha-diversity indices in the digesta but higher alpha-diversity indices in the mucosa. A group of bacterial genera, dominated by members of the *Bacillaceae* family, was enriched in salmon fed the insect meal diet, which confirms our previous findings in a seawater feeding trial. We also found that microbiota in the intestine closely resembled that of the feeds but was distinct from the water microbiota. Notably, bacterial genera associated with the diet effects were also present in the feeds. 

**Conclusions:** We conclude that salmon fed the insect meal diets show consistent changes in the intestinal microbiota. The next challenge is to evaluate the extent to which these alterations are attributable to feed microbiota and dietary nutrients, and what these changes mean for fish physiology and health. 

### Overview

Here's an overview of the file organization in this project.
```
root
├── code
│   ├── 00_setup.ipynb
│   ├── 01_dada2_run1.Rmd
│   ├── 01_dada2_run2.Rmd
│   ├── 02_qiime2_part1.ipynb
│   ├── 03_filtering.Rmd
│   ├── 04_qiime2_part2.ipynb
│   ├── 05_batch_correction.Rmd
│   ├── 06_qiime2_part3.ipynb
│   ├── 07_qiime2R.Rmd
│   ├── 08_taxonomy.Rmd
│   ├── 09_alpha_diversity.Rmd
│   ├── 10_beta_diversity.Rmd
│   ├── 11_multivariable_association.Rmd
│   ├── functions
│   │   ├── plot_prevalence.R
│   │   ├── plot_frequency.R
│   │   └── plot_heatmap.R
│   └── README.md
├── data
│   ├── raw
│   │   ├── casava-18-paired-end-demultiplexed-run1
│   │   ├── casava-18-paired-end-demultiplexed-run2
│   │   ├── qPCR
│   │   └── README.md
│   ├── reference
│   │   ├── mock_description.pdf
│   │   ├── mock_expected.tsv
│   │   ├── sepp-refs-silva-128.qza
│   │   ├── silva_132_99_16S.fna
│   │   ├── silva_132_consensus_taxonomy_l7.txt
│   │   └── README.md
│   ├── intermediate
│   │   ├── dada2
│   │   ├── filtering
│   │   ├── maaslin2
│   │   ├── permanova
│   │   ├── qiime2
│   │   ├── qiime2R
│   │   └── qPCR
│   └── metadata.tsv
├── result
│   ├── figure
│   │   ├── Figure 1.tiff
│   │   ├── Figure 2.tiff
│   │   ├── Figure 3.tiff
│   │   ├── Figure 4.tiff
│   │   ├── Figure 5.tiff
│   │   ├── Figure 6.tiff
│   │   ├── Figure S1.tiff
│   │   ├── Figure S2.tiff
│   │   └── Figure S3.tiff
│   └── table
│       └── Table S1.csv
├── DESCRIPTION
├── Dockerfile
├── Li_AqFl1-Microbiota_2021.Rproj
├── LICENSE.md
└── README.md
```

### How to regenerate the figures and tables
Computationally lightweight RMarkdown files can be directly run online by clicking the ![Launch Binder](http://mybinder.org/badge_logo.svg) badge located at the top of this README file. After clicking the badge, this repository will be turned into an RStudio instance that has all the dependencies installed. The instance has limited computational resources. Tasks requiring intensive computation, i.e., sequence denoising by DADA2, should not be run. Due to technical challenges, the instance was built on R 3.6.3 rather than R 4.1.1. Because of that, some R package versions are different from what we used for the actual data analysis but the results are largely identical. Note that multi-core parallel computing is not available for the RStudio stance we use here. Turn off the parallel computing when you run MaAsLin2.

To reproduce the figures and tables published in the paper, run the following RMarkdown files:

* 03_filtering.Rmd
  * Table S1
* 08_taxonomy.Rmd  
  * Figure 1-2, Figure S1
* 09_alpha_diversity.Rmd
  * Figure 3, Figure S2
* 10_beta_diversity.Rmd
  * Figure 4, Figure S3
  * Table 1
* 11_multivariable_association.Rmd (trun off parallel computing when running MaAsLin2)
  * Figure 5-6
  
### How to regenerate this repository

#### Dependencies and locations

* [Miniconda3](https://docs.conda.io/en/latest/miniconda.html) should be located in your HOME directory.
* [QIIME2 (2020.11)](https://docs.qiime2.org/2020.11/) should be installed within a conda environment named as `qiime2-2020.11`.
  * QIIME2 library: [DEICODE (0.2.3)](https://library.qiime2.org/plugins/deicode/19/) should be installed within the qiime2 conda environment.
  * [grabseqs (0.7.0)](https://github.com/louiejtaylor/grabseqs) should be installed within the qiime2 conda environment.
* [Pandoc (2.5)](https://pandoc.org/index.html) should be located in your PATH.
* [R](https://www.r-project.org/) (4.1.1) should be located in your PATH.
* R packages and versions: see session information at the end of each rmarkdown report.
  
#### Running the analysis

All the code should be run from the project's root directory.

1.Clone this github repository to your local computer.
```bash
# clone the github repository 
git clone https://github.com/yanxianl/Li_AqFl1-Microbiota_2021.git

# enter the project root directory
cd Li_AqFl1-Microbiota_2021

# delete the following folders and the associated files 
rm -rf \
data/intermediate/qiime2/*/core-metrics-results*/ \
data/intermediate/qiime2/*/robust-Aitchison-pca*/ 
```
2.Download raw sequence data, SILVA132 reference database and SILVA128 SEPP reference phylogeny (`code/00_setup.ipynb`).
```bash
# activate qiime2 environment and launch jupyter notebook to run code/00_setup.ipynb interactively
conda activate qiime2-2020.11
jupyter notebook

# shutdown jupyter notebook (ctrl + c) and exit the conda environment
conda deactivate
```
3.Sequence denoising by dada2.
```bash
Rscript -e "rmarkdown::render('code/01_dada2_run1.Rmd')" && Rscript -e "rmarkdown::render('code/01_dada2_run2.Rmd')"
```
4.Taxonomic assignment.
```bash
# activate qiime2 environment
conda activate qiime2-2020.11

# render jupyter notebook
jupyter nbconvert --execute --to html code/02_qiime2_part1.ipynb

# exit the conda environment
conda deactivate
```
5.Filter the feature table to remove: 1).chloroplast/mitochondria sequences and those without a phylum-level taxonomic assignment;
2).low-prevalence features that only present in one sample; 3).contaminating features.
```bash
Rscript -e "rmarkdown::render('code/03_filtering.Rmd')"
```
6.Phylogeny and core-metrics-results.
```bash
# activate qiime2 environment
conda activate qiime2-2020.11

# render jupyter notebook
jupyter nbconvert --execute --to html code/04_qiime2_part2.ipynb

# exit the conda environment
conda deactivate
```
7.Batch effect adjustment.
```bash
Rscript -e "rmarkdown::render('code/05_batch_correction.Rmd')"
```
8.Split core-metrics-results based on the sequencing runs.
```bash
# activate qiime2 environment
conda activate qiime2-2020.11

# render jupyter notebook
jupyter nbconvert --execute --to html code/06_qiime2_part3.ipynb

# exit the conda environment
conda deactivate
```
9.Import qiime2 artifacts into R.
```bash
Rscript -e "rmarkdown::render('code/07_qiime2R.Rmd')"
```
10.Taxonomic analysis.
```bash
Rscript -e "rmarkdown::render('code/08_taxonomy.Rmd')"
```
11.Alpha-diversity analysis.
```bash
Rscript -e "rmarkdown::render('code/09_alpha_diversity.Rmd')"
```
12.Beta-diversity analysis.
```bash
Rscript -e "rmarkdown::render('code/10_beta_diversity.Rmd')"
```
13.Association testing between sample metadata and microbial clades.
```bash
Rscript -e "rmarkdown::render('code/11_multivariable_association.Rmd')"
```

### To-do

* Add a driver script to automate all the analysis, e.g., `make`.

### Acknowledgements

The R package [holepunch](https://karthik.github.io/holepunch/) was used to make the RMarkdown files [binder](https://mybinder.org/)-ready. 

The project organization was inspired by the Riffomonas project. Visit the [*Riffomonas*](http://www.riffomonas.org/) website to check out tutorials on reproducible data analysis for microbiome research.
