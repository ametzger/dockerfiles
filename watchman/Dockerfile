FROM debian:buster AS build

RUN set -e; \
    echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90noninteractive \
    && echo 'DPkg::Options "--force-confnew";' >> /etc/apt/apt.conf.d/90noninteractive \
    && apt-get update \
    && apt-get install --no-install-recommends \
    automake \
    autoconf \
    bash \
    ca-certificates \
    curl \
    build-essential \
    libssl-dev \
    libtool \
    linux-headers-cloud-amd64 \
    pkg-config \
    python-dev \
    && apt-get autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV WATCHMAN_VERSION=4.9.0

RUN cd /tmp \
    && curl --location --output watchman.tar.gz "https://github.com/facebook/watchman/archive/v${WATCHMAN_VERSION}.tar.gz" \
    && tar xzf watchman.tar.gz -C /tmp/ \
    && rm -rf watchman.tar.gz

RUN cd /tmp/watchman-${WATCHMAN_VERSION} \
    && ./autogen.sh \
    && ./configure --enable-lenient \
    && make \
    && make install \
    && cd $HOME \
    && rm -rf /tmp/*

FROM debian:buster-slim AS release

COPY --from=build /usr/local/bin/watchman* /usr/local/bin/
COPY --from=build /usr/local/var/run/watchman /usr/local/var/run/watchman
