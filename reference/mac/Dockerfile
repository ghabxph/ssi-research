FROM ubuntu:18.04

ENV LIBINDY_VERSION 1.15.0-bionic
ENV VERITY_SERVER https://vas.pps.evernym.com

RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    build-essential \
    curl \
    default-jdk \
    iproute2 \
    jq \
    maven \
    python3 \
    python3-pip \
    software-properties-common \
    unzip \
    vim


# Setup apt for Sovrin repository
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 68DB5E88 && \
    add-apt-repository "deb https://repo.sovrin.org/sdk/deb bionic stable"

# Install libindy library from Sovrin repo
RUN apt-get update && apt-get install -y \
    libindy=${LIBINDY_VERSION}

# Install Ngrok
RUN curl -O -s https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip && \
    unzip ngrok-stable-linux-amd64.zip && \
    cp ngrok /usr/local/bin/.

# Install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    apt-get install -y nodejs 

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \ 
    apt-get update && \
    apt-get install -y yarn 

WORKDIR /srv/app

# COPY app.js package.json package-lock.json ./

# COPY public ./public

# Install npm packages
# RUN npm install 2>/dev/null

EXPOSE 3000
