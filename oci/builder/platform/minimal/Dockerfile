ARG DEBIAN_BASE_IMAGE_TAG=stretch-slim
FROM debian:${DEBIAN_BASE_IMAGE_TAG}


ARG BELENIOS_BUILD_DEPENDENCIES='git bubblewrap build-essential libgmp-dev libpcre3-dev pkg-config m4 libssl-dev libsqlite3-dev wget ca-certificates zip unzip libncurses-dev uuid-runtime zlib1g-dev libgd-securityimage-perl cracklib-runtime'
RUN apt-get update -y  && apt-get install -y ${BELENIOS_BUILD_DEPENDENCIES} tree

ARG BELENIOS_OPAM_INIT_ARGS
ENV BELENIOS_OPAM_INIT_ARGS=$BELENIOS_OPAM_INIT_ARGS
# Uninstall any opam package : https://github.com/coq/coq/issues/6746#issuecomment-603584034
RUN apt-get --purge remove opam
RUN apt-get clean && apt-get autoremove
RUN apt-get -f install
RUN dpkg --configure -a



RUN mkdir -p /belenios/src_code

COPY build.sh /belenios
RUN chmod +x /belenios/build.sh

WORKDIR /belenios

CMD [ "/belenios/build.sh" ]
