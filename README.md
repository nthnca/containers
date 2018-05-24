# Containers

## Container for auto building go code

Build the image:

```
git clone https://github.com/nthnca/containers.git
sudo docker build -t nthnca/base base
sudo docker build -t nthnca/builder builder
```

Start a container with our code mapped into it.

```
sudo docker run \
  -v $PWD/:/go/src/github.com/<user>/<repo>/ \
  -v $PWD/build:/go/build --name bx nthnca/builder
```

This will start the builder and should automatically rebuild on any code
changes. CTRL-C should stop it, although you may need to touch a file or
something to get it to wake up.

To restart it after it has been stopped:

```
sudo docker start -a bx
```

And you can copy out the binaries with a command like:

```
sudo docker cp gobuilder:/go/bin/<binary> .
```

## Container for running an appengine service

Build the image:

```
git clone https://github.com/nthnca/containers.git
sudo docker build -t nthnca/base base
sudo docker build -t nthnca/gaedev gaedev
```

Start a container with our code mapped into it.

```
sudo docker run \
  -v $PWD:/go/src/github.com/nthnca/customurls \
  -e YAML=/go/src/github.com/nthnca/customurls/gaeweb/app.yaml \
  --name gaedev -p 80:8080 -p 8000:8000 nthnca/gae
```

This will start the dev_appserver and start serving on port 80.

```
sudo docker start -a bx
```
