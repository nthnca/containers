FROM nthnca/base

ENTRYPOINT (cd /go/src/github.com && go get -v ./...) && exec dev_appserver.py --host=0.0.0.0 --enable_host_checking=false $YAML
