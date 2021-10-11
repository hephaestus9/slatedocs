Provided in the slate repo is a Dockerfile you can use to run slate using [Docker](https://www.docker.com/), as well as providing pre-built images on [Docker Hub](https://hub.docker.com/r/slatedocs/slate). Docker is similar to Vagrant in that it provides a reproducible, portable development environment using virtualization, however it does not provide a full VM, rather piggy backing off the host, allowing for a slimmer installation profile than Vagrant / full VMs. However, Docker does come with a number of its own terms, and for beginners, we recommend looking at
[this Glossary](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/docker-terminology)
to familiarize yourself with some of them.

## Dependencies

* [Docker](https://www.docker.com/), see [this page](https://www.docker.com/get-started) for installing Docker Desktop.

## Getting Started

1. Fork this repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/slate.git`
3. `cd slate`
4. Grab the slate image (`docker pull slatedocs/slate`) or build the docker image for the repository (`docker build . -t slatedocs/slate`).

Note: If you are using the pre-built images for Slate, you may wish to remove all files other than the `source` directory from your repository.

## Building Slate

To use Docker to just build your site, run:

```
docker run --rm --name slate -v $(pwd)/build:/srv/slate/build -v $(pwd)/source:/srv/slate/source slatedocs/slate build
```

After this command completes, you should see the built artifacts for your site in the `$(pwd)/build` directory, which you can then statically serve for your website.

_Note_: You may omit the final `build` argument and get the same result. By default, if given no command, the Dockerfile will run `build`.

## Running Slate

If you wish to run the development server for Slate to aid in working on the site, run:

```
docker run --rm --name slate -p 4567:4567 -v $(pwd)/source:/srv/slate/source slatedocs/slate serve
```

and you will be able to access your site at http://localhost:4567 until you stop the running container process.

## Advanced Usage

The provided Docker images contain the full Slate environment and all related files. This means that you may
provide as much or as little as you want into the container while utilizing defaults. For example, if you only
wanted to include your markdown sources and not overwrite the default JS, CSS, etc. you may wish to use the
following mount options:

```
-v $(pwd)/source/index.html.md:/srv/slate/source/index.html.md -v $(pwd)/source/includes:/srv/slate/source/includes
```

## What Now?

The next step is to [learn how to edit `source/index.html.md` to change the content of your docs](Markdown-Syntax). Once you're done, you might want to think about [deploying your docs](https://github.com/slatedocs/slate/wiki/Deploying-Slate).