# Use official Ubuntu 20.04 image as base
FROM ubuntu:20.04

# Set working directory
WORKDIR /app

# Set noninteractive shell
RUN DEBIAN_FRONTEND=noninteractive

# Update package list and install system dependencies
RUN apt-get update \
    && apt-get install -y \
        git \
        python3 \
        make \
        gcc \
        pkg-config \
        build-essential \
        libx11-dev \
        libxkbfile-dev \
        libsecret-1-dev \
    && apt-get clean

# Install Node.js
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

# Copy package.json and yarn.lock
COPY package.json yarn.lock ./

# Install Node.js dependencies
RUN yarn install

# Copy rest of the application code
COPY . .

# Build the Theia app
RUN yarn theia build

# Expose port for Theia app
EXPOSE 3000

# Start the Theia app
CMD [ "yarn", "theia", "start", "/app", "--hostname=0.0.0.0" ]
