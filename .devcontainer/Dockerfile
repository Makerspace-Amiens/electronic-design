FROM ruby:3.3-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    openssh-client \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN gem install bundler

WORKDIR /workspace
