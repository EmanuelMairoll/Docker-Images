FROM kathara/base
LABEL org.opencontainers.image.authors="Network Security Group, ETH Zurich <netsec.ethz.ch>"

# Install SCION from GitHub release
ARG DEBIAN_FRONTEND="noninteractive"
ARG TARGETARCH

WORKDIR /tmp

RUN wget https://github.com/scionproto/scion/releases/download/v0.12.0/scion_0.12.0_deb_$TARGETARCH.tar.gz && \
    tar xfz scion_0.12.0_deb_$TARGETARCH.tar.gz && \
    apt install ./scion*.deb && \
    apt clean && \
    rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/*

# Strip templating from systemd service files, systemd-replacement-script does not support it
RUN mv /usr/lib/systemd/system/scion-router\@.service /usr/lib/systemd/system/scion-router.service && \
    sed -i 's/%i/br/g' /usr/lib/systemd/system/scion-router.service && \
    mv /usr/lib/systemd/system/scion-control\@.service /usr/lib/systemd/system/scion-control.service && \
    sed -i 's/%i/cs/g' /usr/lib/systemd/system/scion-control.service
