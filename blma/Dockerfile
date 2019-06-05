FROM rocker/tidyverse

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

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
    valgrind \
    vim
ENV GSL_CBLAS_LIB=-lopenblas


RUN mkdir -p ~/.R && \
	echo 'CPPFLAGS= -Wno-ignored-attributes' >> ~/.R/Makevars && \
	echo 'PKG_LIBS+=-pthread' >> ~/.R/Makevars

# Install dependencies for blma
RUN Rscript -e "install.packages('RcppEigen')"
RUN Rscript -e "install.packages('RcppGSL')"

# Install test dependencies for blma
RUN Rscript -e "install.packages('glue')"
RUN Rscript -e "install.packages('tictoc')"

# Set working directory
WORKDIR /blma

# Install blma itself
RUN git clone https://github.com/certifiedwaif/blma.git /blma/
RUN R -e 'Rcpp::compileAttributes()'
RUN R -e 'devtools::document()'
RUN R -e 'devtools::install(quick=T)'

CMD ["R"]
