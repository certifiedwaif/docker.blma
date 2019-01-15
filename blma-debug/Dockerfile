FROM certifiedwaif/blma-base:latest

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

# Set working directory
WORKDIR /blma/

# Install blma itself
RUN git clone https://github.com/certifiedwaif/blma.git /blma/
RUN R -e 'Rcpp::compileAttributes()'
RUN R -e 'devtools::document()'
RUN R -e 'devtools::install(quick=T)'

CMD ["R", "-d", "gdb"]
