FROM golang:1

LABEL description="My golang development enviroment." by="yokonsan"

ENV DEBIAN_FRONTEND=noninteractive
ENV GO111MODULE=on
ENV GOPROXY=https://goproxy.io
RUN apt-get update -y \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1

# Verify git, process tools, lsb-release (common in install instructions for CLIs) installed.
RUN apt-get -y install git iproute2 procps lsb-release

# Install Go tools.
# Install gocode-gomod.
RUN go get -u -v github.com/nsf/gocode \
    && go get -u -v github.com/rogpeppe/godef \
    && go get golang.org/x/lint/golint \
    && go get -u -v github.com/lukehoban/go-find-references \
    && go get -u -v github.com/lukehoban/go-outline \
    && go get -u -v sourcegraph.com/sqs/goreturns \
    && go get -u -v golang.org/x/tools/cmd/gorename \
    && go get -u -v github.com/tpng/gopkgs \
    && go get -u -v github.com/newhook/go-symbols \
    && go get -u -v github.com/zmb3/gogetdoc \
    && go get -u -v golang.org/x/tools/cmd/guru \
    && go get -u -v github.com/go-delve/delve/cmd/dlv \
    && go get -u -v golang.org/x/tools/cmd/goimports \
    && go get -v golang.org/x/tools/gopls 2>&1 \
    # Clean up.
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Revert workaround at top layer.
ENV DEBIAN_FRONTEND=dialog

# Expose service ports.
EXPOSE 8000