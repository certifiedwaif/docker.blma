FROM ubuntu:18.04
# FROM ubuntu:21.10

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y gnupg software-properties-common
RUN apt-get update && apt-get install -y \
	r-base \
	r-base-dev
RUN apt-get update && apt-get install -y \
	gdb \
    git \
    libcurl4-gnutls-dev \
    libgit2-dev \
	libgsl-dev \
	libopenblas-dev \
    libssl-dev \
    libxml2-dev \
    valgrind \
    vim
ENV GSL_CBLAS_LIB=-lopenblas

RUN mkdir -p ~/.R && \
	echo 'PKG_LIBS+=-pthread' >> ~/.R/Makevars

# Install dependencies for blma
RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('roxygen2')"

RUN Rscript -e "install.packages('BH')"
RUN Rscript -e "install.packages('RcppEigen')"
RUN Rscript -e "install.packages('RcppGSL')"

RUN Rscript -e "install.packages('glue')"
RUN Rscript -e "install.packages('tictoc')"
RUN Rscript -e "install.packages('testthat')"

# Set working directory
WORKDIR /blma

# Install blma itself
RUN git clone -b fix-data-sharing https://github.com/certifiedwaif/blma.git /blma/
RUN R -e 'Rcpp::compileAttributes()'
RUN R -e 'devtools::document()'
RUN R -e 'devtools::install(quick=T)'

# Install dependencies for John's test scripts
RUN R -e "install.packages('BAS')"
RUN R -e "install.packages('BayesVarSel')"
RUN R -e "install.packages('BMS')"
RUN R -e "install.packages('gsl')"
RUN R -e "devtools::install_github('cran/appell')"
RUN R -e "install.packages('pracma')"
WORKDIR /test.blma
RUN git clone https://github.com/certifiedwaif/test.blma.git /test.blma/

# Install dependencies for blmatest, and blmatest
RUN R -e "install.packages('data.table')"
RUN R -e "install.packages('ncvreg')"
WORKDIR /blmatest
RUN git clone https://github.com/certifiedwaif/blmatest.git /blmatest/
RUN R -e 'Rcpp::compileAttributes()'
RUN R -e 'devtools::install(quick=T)'

# Build shared libraries, and put them in the proper dir
WORKDIR /blmatest/src
RUN R CMD SHLIB hyperGonN.c posroot.c
RUN R CMD SHLIB ZS.c posroot.c
RUN cp /blmatest/src/hyperGonN.so /test.blma/Common/
RUN cp /blmatest/src/ZS.so /test.blma/Common/

WORKDIR /blma
CMD ["R"]
