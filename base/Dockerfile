FROM ubuntu:18.04

ENV CLOUD_SDK_VERSION 198.0.0
ENV GOPATH /home/builder/go:/go

RUN apt-get -qqy update && apt-get install -qqy \
        curl \
        apt-transport-https \
        lsb-release \
        openssh-client \
        inotify-tools \
        git \
        golang-go \
        gnupg gnupg2 && \
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

RUN useradd -ms /bin/dash builder && \
    mkdir /go && \
    chown builder /go && \
    apt-get update && \
    apt-get install -y google-cloud-sdk=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-app-engine-go=${CLOUD_SDK_VERSION}-0 && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud --version

USER builder
WORKDIR /home/builder

# Preload some of this so every container doesn't have to get it.
RUN go get cloud.google.com/go google.golang.org/api/datastore/v1
