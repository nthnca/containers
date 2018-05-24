FROM nthnca/base

RUN useradd -ms /bin/dash builder
RUN mkdir /go
RUN chown builder /go

USER builder
WORKDIR /home/builder
ADD run run

RUN go get cloud.google.com/go google.golang.org/api/datastore/v1
#google.golang.org/api golang.org/x cloud.google.com/go

ENTRYPOINT [ "/home/builder/run" ]
