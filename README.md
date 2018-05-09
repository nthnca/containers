# Containers

## Container for auto building go code

First we need to build the container into a image.

```
git clone https://github.com/nthnca/containers.git
sudo docker build -t nthnca/gobuilder gobuilder
```

Then start a container with our code mapped into it.

```
sudo docker run
  -v $PWD/:/go/src/github.com/<user>/<repo>/
  -v $PWD/build:/go/build --name gobuilder -d nthnca/gobuilder
```
