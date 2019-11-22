BootStrap: shub
From: granek/singularity-rstudio-tidyverse:3.6.0

%labels
  Maintainer Marc J Williams
#  RStudio_Version 1.1.463

%help
  This will run RStudio Server with tidyverse and support for knitting plus pandoc for document conversion. Also included are a collection of bioconductor packages for single cell analysis

%apprun rserver
  exec rserver "${@}"

%runscript
  exec rserver "${@}"

%environment
  export PATH=/usr/lib/rstudio-server/bin:${PATH}

%post
   apt-get update && \
   apt-get install -y build-essential git curl wget &&\
   apt-get install -y tzdata language-pack-ja &&\
   apt-get install -y texlive-base texlive-lang-japanese texlive-luatex latexmk xzdec pandoc nano
   apt-get clean
   update-locale LANG=ja_JP.UTF8
   dpkg-reconfigure tzdata

   # Install some other useful R packages
    Rscript -e "install.packages(pkgs = c('RColorBrewer', 'devtools', 'cowplot', 'rmarkdown', 'gtools', 'argparse', 'uwot', 'fuzzyjoin', 'dbscan', 'jcolors', 'ggthemes', 'viridis', 'knitr', 'entropy', 'clues', 'aricode', 'BiocManager', 'igraph', 'deconstructSigs', 'pracma', 'ClusterR'), \
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
