FROM ubuntu:16.04 as builder
# Build environment

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Base
RUN apt-get update
RUN apt-get install -y \
	git \
	nano \
	curl \
	build-essential \
	libssl-dev \
	npm \
	nodejs \
	nodejs-legacy \
	libgmp3-dev

#WORKDIR /root/
ENV NVM_VERSION v0.10.25
ENV NODE_VERSION v7.5.0
ENV NVM_DIR /usr/local/nvm
RUN mkdir $NVM_DIR
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

ENV NODE_PATH $NVM_DIR/$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/$NODE_VERSION/bin:$PATH

RUN (echo "source $NVM_DIR/nvm.sh && \
    nvm install $NODE_VERSION && \
    nvm alias default $NODE_VERSION && \
    nvm use default" | bash && \
    git clone https://github.com/buzzkillb/node-open-mining-portal.git && \
    cd node-open-mining-portal && \
    npm update && \
    rm -rf pool_configs && \
    rm config_example.json)

CMD ["node", "init.js"]
