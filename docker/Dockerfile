# Copied from https://github.com/j-rivero/jetty_testing/blob/main/Dockerfile
FROM ubuntu:noble AS jetty-prerelease
ENV LANG=C
ENV LC_ALL=C
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y dirmngr git python3 python3-docopt python3-yaml python3-distro \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/gazebo-tooling/gzdev \
    && cd gzdev \
    && python3 gzdev.py repository enable osrf stable \
    && python3 gzdev.py repository enable osrf prerelease 
RUN apt-get install -y gz-jetty \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
