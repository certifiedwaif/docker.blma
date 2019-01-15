FROM certifiedwaif/blma-base:latest

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

WORKDIR /blma/

RUN git clone https://github.com/certifiedwaif/blma.git /blma/
RUN R -e 'Rcpp::compileAttributes()'
RUN R -e 'devtools::document()'
RUN R -e 'devtools::install()'

#CMD ["R", "-d", "gdb"]
CMD ["R"]
