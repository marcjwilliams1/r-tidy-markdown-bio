BootStrap: shub
From: granek/singularity-rstudio-tidyverse:3.5.2

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
    Rscript -e "install.packages(pkgs = c('devtools', 'cowplot', 'rmarkdown', 'gtools', 'argparse', 'uwot', 'fuzzyjoin', 'dbscan', 'jcolors', 'ggthemes', 'viridis', 'knitr', 'entropy', 'clues', 'aricode'), \
      repos='https://cran.revolutionanalytics.com/', \
      dependencies=TRUE, \
      clean = TRUE)"

   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                     biocLite('scran')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                      biocLite('scater')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                    biocLite('GenomicRanges')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                     biocLite('IRanges')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                     biocLite('rtracklayer')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                   biocLite('GenVisR')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                    biocLite('Biostrings')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                  biocLite('SingleCellExperiment')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                   biocLite('edgeR')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                   biocLite('Rsamtools')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                   biocLite('seqinr')"

   Rscript -e "library(devtools); install_github('im3sanger/dndscv')"
   Rscript -e "library(devtools); install_github('Irrationone/cellassign')"
   Rscript -e "library(devtools); install_github('VPetukhov/ggrastr')"

%runscript
pandoc "$@"
