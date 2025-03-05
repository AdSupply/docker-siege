forked from [ecliptik/docker-siege](https://github.com/ecliptik/docker-siege)

## Running Container as a Command

The [Dockerfile](Dockerfile) has a default `ENTRYPOINT` of `siege` and all arguments passed after the container image will pass to `siege`. The default argument is `--help`.

## Running Container With Local Configuration

To skip the bundled configuration files in the image, and use local files in the current directoy, bind mount it to `/app` using the `-v` flag.

For example using this repository and you want to create a URL list to pass to siege called `urls.txt` without having to re-build the container image,

```
docker run -it --rm -v $(pwd):/app docker-siege -c 50 -f /app/urls.txt -R /app/siege.conf
```

The `-v $(pwd):/app` will bind mount your current directory to `/app` within the container, letting you use local files.

## Running Container Interactively

You can start the container and attach a console to run siege interactively.

```
docker run -it --rm --entrypoint=/bin/bash docker-siege:latest
```

## Updating Docker Image

To update the version fo Siege, find the latest version from the [Siege Downloads](https://download.joedog.org/siege/) page and in the [Dockerfile](Dockerfile) update the `SIEGE_VERSION` variable and re-build,

```
docker build -t docker-siege .
```
