FROM ubuntu:bionic

USER root

ENV UBUNTU_CODENAME=bionic \
    LANG=en_US.UTF-8 \
    DEBIAN_FRONTEND=noninteractive \
    ERL_VERSION=22.2-1 \
    ELIXIR_VERSION=1.9.4 \
    ASDF=false

# Base build deps
RUN apt-get update -q \
    && LANG=C apt-get -qq install locales \
    && locale-gen "$LANG" \
    && apt-get -qq upgrade \
    && apt-get -qq install dialog apt-utils \
    && apt-get -qq install \
        awscli \
        curl \
        git \
        make \
        unzip \
        wget

# Install Erlang, Elixir and Node.js
RUN apt-get -qq install \
        libc6 \
        libgcc1 \
        libncurses5 \
        libsctp1 \
        libssl1.0 \
        libstdc++6 \
        libwxbase3.0-0v5 \
        libwxgtk3.0-0v5 \
        procps \
    && apt-get -f install \
    && wget --no-verbose -P /tmp/ "https://packages.erlang-solutions.com/erlang/debian/pool/esl-erlang_${ERL_VERSION}~ubuntu~bionic_amd64.deb" \
    && dpkg -i "/tmp/esl-erlang_${ERL_VERSION}~ubuntu~${UBUNTU_CODENAME}_amd64.deb" \
    && wget --no-verbose -P /tmp/ "https://github.com/elixir-lang/elixir/releases/download/v${ELIXIR_VERSION}/Precompiled.zip" \
    && unzip -q /tmp/Precompiled.zip -d /usr/local \
    && apt-get -qq install nodejs npm \
    && apt-get -f install
