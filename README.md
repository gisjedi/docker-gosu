# docker-gosu
Docker base images using gosu with custom support for on-demand chowning to user:group

## How to use this image

### Create a `Dockerfile` in your application requring explicit user:group execution

```dockerfile
FROM gisjedi/centos-gosu:7

ENV GOSU_USER 99:50
ENV GOSU_CHOWN /opt/gosu

RUN mkdir -p /opt/gosu

CMD [ "id" ]
```

You can then build and run the Docker image:

```console
$ docker build -t my-gosu-app .
$ docker run -it --rm my-gosu-app
```

### Run a simple command with gosu container 

For many simple use cases, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a single command by using the image directly:

```console
$ mkdir -p "$PWD"/gosu
$ chown -R 99:50 "$PWD"/gosu
$ docker run -it --rm -e GOSU_USER=99:50 -e GOSU_CHOWN=/tmp/gosu -v "$PWD"/gosu:/tmp/gosu gisjed/centos-gosu ls -lh /tmp/gosu
```
