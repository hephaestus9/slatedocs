Provided in the slate repo is a Dockerfile you can use to run slate using [Docker](https://www.docker.com/). Docker is similar to Vagrant in that it provides a reproducible, portable development environment using virtualization, however it does not provide a full VM, rather piggy backing off the host, allowing for a slimmer installation profile than Vagrant / full VMs. However, Docker does come with a number of its own terms, and for beginners, we recommend looking at
[this Glossary](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/docker-terminology)
to familiarize yourself with some of them.

## Dependencies

* [Docker](https://www.docker.com/), see [this page](https://www.docker.com/get-started) for installing Docker Desktop.

## Getting Started

1. Fork this repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/slate.git`
3. `cd slate`
4. Build the docker image for slate: `docker build . -t slate`

## Running Slate

To start a container for slate, run:

```
docker run -it -d --rm --name -v $(pwd)/build:/srv/slate/build -v $(pwd)/source:/srv/slate/source slate
```

and you will be able to access your site at http://localhost:4567.

To build your sources while the container is running, run:

```
docker exec -it slate /bin/bash -c "bundle exec middleman build"
```

## Stopping Slate

To stop the slate container, run:

```bash
docker stop slate
```

## What Now?

The next step is to [learn how to edit `source/index.md` to change the content of your docs](Markdown-Syntax). Once your done, you might want to think about [deploying your docs](https://github.com/slatedocs/slate/wiki/Deploying-Slate).