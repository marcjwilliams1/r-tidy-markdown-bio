BootStrap: shub
From: nickjer/singularity-rstudio:3.5.2

%labels
  Maintainer Marc J Williams
#  RStudio_Version 1.1.463

%help
  This will run RStudio Server with tidyverse and support for knitting

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
   apt-get install -y texlive-base texlive-lang-japanese texlive-luatex latexmk xzdec pandoc
   apt-get install -y cargo
   apt-get install -y libmagick++-dev
   apt-get install -y python
   apt-get install -y libpython-dev
   apt-get install -y libpython3-dev
   apt-get clean
   update-locale LANG=ja_JP.UTF8
   dpkg-reconfigure tzdata

   # Install tidyverse and other packages
    Rscript -e "install.packages(pkgs = c('tidyverse','caTools', 'devtools', 'rprojroot', 'cowplot', 'rmarkdown', 'gtools', 'argparse', 'uwot', 'fuzzyjoin', 'viridis', 'dbscan', 'reticulate', 'tensorflow', 'jcolors', 'ggthemes', 'viridis', 'knitr'), \
      repos='https://cran.revolutionanalytics.com/', \
      dependencies=TRUE, \
      clean = TRUE)"

   script -e "tensorflow::install_tensorflow()"

   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                     biocLite('scran')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                      biocLite('scater')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                    biocLite('GenomicRanges')"
   R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                     biocLite('IRanges')"
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
