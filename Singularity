BootStrap: docker
From: rocker/tidyverse

%labels
  Maintainer Marc J Williams
#  RStudio_Version 1.1.463

%help
  This will run RStudio Server with tidyverse and support for knitting plus pandoc for document conversion. Also included are a collection of bioconductor packages for single cell analysis

%post

   # Install some other useful R packages
    Rscript -e "install.packages(pkgs = c('RColorBrewer', 'cowplot', 'gtools', 'argparse', 'uwot', 'fuzzyjoin', 'dbscan', 'jcolors', 'ggthemes', 'viridis', 'entropy', 'clues', 'aricode', 'BiocManager', 'igraph', 'deconstructSigs', 'pracma', 'ClusterR', 'HMM', 'circlize', 'VGAM'), \
      repos='https://cran.revolutionanalytics.com/', \
      dependencies=TRUE, \
      clean = TRUE)"

   R -e "BiocManager::install('scran')"
   R -e "BiocManager::install('scater')"
   R -e "BiocManager::install('GenomicRanges')"
   R -e "BiocManager::install('IRanges')"
   R -e "BiocManager::install('rtracklayer')"
   R -e "BiocManager::install('GenVisR')"
   R -e "BiocManager::install('Biostrings')"
   R -e "BiocManager::install('SingleCellExperiment')"
   R -e "BiocManager::install('edgeR')"
   R -e "BiocManager::install('Rsamtools')"
   R -e "BiocManager::install('seqinr')"
   R -e "BiocManager::install('copynumber')"
   R -e "BiocManager::install('QDNAseq')"
   R -e "BiocManager::install('QDNAseq.hg19')"
   R -e "BiocManager::install('ggtree')"
   R -e "BiocManager::install('ComplexHeatmap')"
   R -e "BiocManager::install('org.Hs.eg.db')"
   R -e "BiocManager::install('TxDb.Hsapiens.UCSC.hg19.knownGene')"
   R -e "BiocManager::install('BSgenome.Hsapiens.UCSC.hg19')"


   Rscript -e "library(devtools); install_github('im3sanger/dndscv')"
   Rscript -e "library(devtools); install_github('VPetukhov/ggrastr')"
   Rscript -e "library(devtools); install_github('FunGeST/Palimpsest')"

%runscript
pandoc "$@"
