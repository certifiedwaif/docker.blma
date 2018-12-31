FROM rocker/r-base:latest
LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

## Update and install extra packages
RUN apt-get update \
  && apt-get install -y \
    libglu1-mesa-dev \
    libgsl0-dev \
    libomp-dev \
    mesa-common-dev\
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/

## Add in opts
# Global site-wide config for clang
RUN mkdir -p $HOME/.R/ \
#    && echo "MAKEFLAGS = -j 8"	>> $HOME/.R/Makevars \
	&& echo "CPPFLAGS= -Wno-ignored-attributes" >> $HOME/.R/Makevars

## Add in required R packages
RUN . /etc/environment \
  && install2.r --error \
  remotes

# Install github packages
RUN installGithub.r \
    --deps "TRUE" \
    certifiedwaif/blma

# Remove unnecessary tmp files
RUN rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# Set working directory
WORKDIR /home/blma
