FROM buildpack-deps:bookworm-scm

ARG TEXLIVE_MIRROR=https://mirror.math.princeton.edu/pub/CTAN/systems/texlive/tlnet/

WORKDIR /texlive-install

COPY ./texlive.profile .

RUN wget ${TEXLIVE_MIRROR}/install-tl-unx.tar.gz \
  && tar -xf install-tl-unx.tar.gz --strip-components 1 \
  && ./install-tl -profile texlive.profile --location ${TEXLIVE_MIRROR}\
  && /usr/local/texlive/????/bin/*/tlmgr path add

RUN apt update && apt install -y build-essential
RUN curl -Lk http://xrl.us/cpanm -o /usr/bin/cpanm && chmod +x /usr/bin/cpanm

RUN <<EOF
  cpanm -n Log::Log4perl
  cpanm -n YAML/Tiny.pm
  cpanm -n Log::Dispatch::File
  cpanm -n File::HomeDir
  cpanm -n Unicode::GCString
EOF

WORKDIR /

RUN rm -rf /texlive-install
