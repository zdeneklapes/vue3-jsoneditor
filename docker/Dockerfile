# syntax=docker/dockerfile:1

# -------------------------------------
# Base image with Node.js and pnpm
# -------------------------------------
FROM node:24-bookworm as frontend
ENV WORKDIR /opt/frontend
WORKDIR $WORKDIR

# Install development tools
RUN apt-get update && apt-get install -y \
    fish \
    vim \
    git \
    curl \
    wget \
    tree \
    && rm -rf /var/lib/apt/lists/*

# Install global npm tools
RUN npm install -g pnpm && \
    mkdir -p /root/.config/fish/completions && \
    pnpm completion fish > /root/.config/fish/completions/pnpm.fish
