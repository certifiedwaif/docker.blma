FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive
RUN sed -i 's|http://archive.ubuntu.com|http://au.archive.ubuntu.com|g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
	gdb \
	libgsl-dev \
    git \
    libcurl4-gnutls-dev \
    libgit2-dev \
    libssl-dev \
    libxml2-dev \
    r-base \
    valgrind
RUN echo 'local({r <- getOption("repos") \n\
       r["CRAN"] <- "https://cran.csiro.au"  \n\
       options(repos=r) \n\
})'\
> ~/.Rprofile
RUN mkdir -p ~/.R && echo 'CPPFLAGS= -Wno-ignored-attributes' > ~/.R/Makevars
RUN mkdir -p ~/.R && echo 'MAKEFLAGS= -j 4' >> ~/.R/Makevars

# Install dependencies for building, documenting and testing
RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('roxygen2')"
RUN Rscript -e "install.packages('testthat')"

# Install the development version of devtools
RUN Rscript -e "devtools::install_github('r-lib/devtools')"

# Install dependencies for blma
RUN Rscript -e "install.packages('BH')"
RUN Rscript -e "install.packages('Rcpp')"
RUN Rscript -e "install.packages('RcppEigen')"
RUN Rscript -e "install.packages('RcppGSL')"
