FROM liuchong/rustup:1.53.0-musl

RUN apt-get update
RUN apt-get install -y \
    build-essential \
    cmake \
    libxml2-dev \
    libssl-dev \
    git \
    wget \
    clang \
    gcc \
    g++ \
    zlib1g-dev \
    libmpc-dev \
    libmpfr-dev \
    libgmp-dev

RUN git clone https://github.com/tpoechtrager/osxcross \
    && cd osxcross \
    && curl -O https://s3.dockerproject.org/darwin/v2/MacOSX10.10.sdk.tar.xz \
    && mv MacOSX10.10.sdk.tar.xz tarballs/ \
    && UNATTENDED=yes OSX_VERSION_MIN=10.7 ./build.sh

ENV PATH="/root/osxcross/target/bin:${PATH}"