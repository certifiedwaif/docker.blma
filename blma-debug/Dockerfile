FROM certifiedwaif/blma-base:latest

LABEL maintainer="Mark Greenaway"
LABEL email="certifiedwaif@gmail.com"

# Set working directory
WORKDIR /blma/
COPY ./blma/ /blma/
RUN ./build.sh

COPY .gdbinit /blma/
COPY eigen/ /blma/eigen/

CMD ["R", "-d", "gdb"]
