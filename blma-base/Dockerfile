FROM rocker/tidyverse
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y \
	gdb \
    git \
    libcurl4-gnutls-dev \
    libgit2-dev \
	libgsl-dev \
	libopenblas-dev \
    libssl-dev \
    libxml2-dev \
    r-base \
    valgrind \
    vim
ENV GSL_CBLAS_LIB=-lopenblas
RUN echo 'local({r <- getOption("repos") \n\
       r["CRAN"] <- "https://cran.csiro.au"  \n\
       options(repos=r) \n\
})'\
> ~/.Rprofile


RUN mkdir -p ~/.R && \
	echo 'CPPFLAGS= -Wno-ignored-attributes' >> ~/.R/Makevars && \
	echo 'PKG_LIBS+=-pthread' >> ~/.R/Makevars

# Install the development version of devtools
RUN Rscript -e "devtools::install_github('r-lib/devtools')"

# Install dependencies for blma
RUN Rscript -e "install.packages('RcppEigen')"
RUN Rscript -e "install.packages('RcppGSL')"

# Install test dependencies for blma
RUN Rscript -e "install.packages('glue')"
RUN Rscript -e "install.packages('tictoc')"
