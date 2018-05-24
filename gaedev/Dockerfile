FROM nthnca/base

RUN useradd -ms /bin/dash builder
RUN mkdir /go
RUN chown builder /go

USER builder
WORKDIR /home/builder

# Preload some of this so every container doesn't have to get it.
RUN go get cloud.google.com/go google.golang.org/api/datastore/v1

ENTRYPOINT (cd /go/src/github.com && go get -v ./...) && exec dev_appserver.py --host=0.0.0.0 --enable_host_checking=false $YAML
