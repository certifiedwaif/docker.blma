FROM rocker/tidyverse:latest

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

## Update and install extra packages
ENV DEBIAN_FRONTEND noninteractive
RUN sed -i 's|http://archive.ubuntu.com|http://au.archive.ubuntu.com|g' /etc/apt/sources.list
RUN apt-get update \
  && apt-get install -y \
    libglu1-mesa-dev \
    libgmp-dev \
    libgsl0-dev \
    libomp-dev \
    mesa-common-dev\
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/

# Set CRAN repo
RUN echo 'local({r <- getOption("repos") \n\
       r["CRAN"] <- "http://cran.csiro.au"  \n\
       options(repos=r) \n\
})'\
> ~/.Rprofile

## Add in opts
# Global site-wide config for clang
RUN mkdir -p $HOME/.R/ \
    && echo "MAKEFLAGS = -j 4"	>> $HOME/.R/Makevars \
	&& echo "CPPFLAGS= -Wno-ignored-attributes" >> $HOME/.R/Makevars

# Install blma itself
RUN Rscript -e "devtools::install_github('certifiedwaif/blma')"

# Set working directory
WORKDIR /home/blma

CMD ["R"]
