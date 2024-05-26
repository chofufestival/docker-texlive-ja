FROM buildpack-deps:bookworm-scm

ARG TEXLIVE_MIRROR=https://mirror.math.princeton.edu/pub/CTAN/systems/texlive/tlnet/

WORKDIR /texlive-install

COPY ./texlive.profile .

RUN wget ${TEXLIVE_MIRROR}/install-tl-unx.tar.gz \
  && tar -xf install-tl-unx.tar.gz --strip-components 1 \
  && ./install-tl -profile texlive.profile --location ${TEXLIVE_MIRROR}\
  && /usr/local/texlive/????/bin/*/tlmgr path add

WORKDIR /

RUN rm -rf /texlive-install
