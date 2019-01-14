FROM certifiedwaif/blma-base:latest

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

# Install blma itself
RUN Rscript -e "devtools::install_github('certifiedwaif/blma')"

# Set working directory
WORKDIR /blma

CMD ["R"]
