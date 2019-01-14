FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive
RUN sed -i 's|http://archive.ubuntu.com|http://au.archive.ubuntu.com|g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
    gdb \
    git \
    libcurl4-gnutls-dev \
    libgit2-dev \
	libgsl-dev \
    libssl-dev \
    libxml2-dev \
    r-base \
    valgrind
RUN echo 'local({r <- getOption("repos") \n\
       r["CRAN"] <- "http://cran.r-project.org"  \n\
       options(repos=r) \n\
})'\
> ~/.Rprofile
RUN mkdir -p ~/.R && echo 'CPPFLAGS= -Wno-ignored-attributes' > ~/.R/Makevars

# Install dependencies for building, documenting and testing
RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('roxygen2')"
RUN Rscript -e "install.packages('testthat')"

# Install dependencies for blma
RUN Rscript -e "install.packages('BH')"
RUN Rscript -e "install.packages('Rcpp')"
RUN Rscript -e "install.packages('RcppEigen')"
RUN Rscript -e "install.packages('RcppGSL')"

WORKDIR /blma/

RUN git clone https://github.com/certifiedwaif/blma.git /blma/
RUN R -e 'Rcpp::compileAttributes()'
RUN R -e 'devtools::document()'
RUN R -e 'devtools::install()'

CMD ["R", "-d", "gdb"]
