FROM ubuntu:22.04

ENV RUST_VERSION=1.87.0 \
    BUF_VERSION=1.38.0

RUN apt-get update && \
    apt-get install -y \
        build-essential \
        curl

# Github unsets `$HOME` so we set the variables below to stop `rustup` using it.
RUN mkdir /usr/local/rustup
RUN mkdir /usr/local/cargo
ENV RUSTUP_HOME=/usr/local/rustup
ENV CARGO_HOME=/usr/local/cargo

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y
ENV PATH="/usr/local/cargo/bin:$PATH"

RUN rustup install ${RUST_VERSION}
RUN rustup default stable
RUN rustup component add rustfmt
RUN rustup component add clippy

# Install buf
RUN curl -sSL "https://github.com/bufbuild/buf/releases/download/v${BUF_VERSION}/buf-$(uname -s)-$(uname -m)" -o "/usr/local/bin/buf"
RUN chmod +x "/usr/local/bin/buf"

CMD ["cargo"]
