FROM ubuntu:latest
MAINTAINER Nathan Bullock “nathanbullock@gmail.com”
RUN apt-get update && apt-get install -y \
  golang-go \
  inotify-tools \
  git

RUN useradd -ms /bin/dash builder
RUN mkdir /go
RUN chown builder /go

USER builder
WORKDIR /home/builder
ADD run run

ENV GOPATH /home/builder/go:/go

ENTRYPOINT [ "/home/builder/run" ]
