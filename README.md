# Containers

## Container for auto building go code

First we need to build the container into an image.

```
git clone https://github.com/nthnca/containers.git
sudo docker build -t nthnca/gobuilder gobuilder
```

Then start a container with our code mapped into it.

```
sudo docker run \
  -v $PWD/:/go/src/github.com/<user>/<repo>/ \
  -v $PWD/build:/go/build --name gobuilder -d nthnca/gobuilder
```

You can watch the output with a command like:

```
sudo docker logs gobuilder
```

And you can copy out the binaries with a command like:

```
sudo docker cp gobuilder:/go/bin/<binary> .
```
