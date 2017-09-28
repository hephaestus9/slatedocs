Some people have had success with Docker, although it is not officially supported. You'll need to create three files in your Slate directory:

#### .dockerignore :

    .git
    source

#### Dockerfile :

    FROM ruby:2.3.1-onbuild
    MAINTAINER Adrian Perez <adrian@adrianperez.org>
    VOLUME /usr/src/app/source
    EXPOSE 4567

    RUN apt-get update && apt-get install -y nodejs \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

    CMD ["bundle", "exec", "middleman", "server", "--watcher-force-polling"]

#### docker-compose.yml :

```yaml
app:
  build: .
  ports:
    - 4567:4567
  volumes:
    - ./source:/usr/src/app/source
```

After the files have been created, you can run Slate with `docker-compose up`.

You can now see the docs at http://localhost:4567. Whoa! That was fast!

To build a local static copy of your API documentation into the `build` directory, run

    docker run --rm -v $PWD:/usr/src/app/source -w /usr/src/app/source slate_app bundle exec middleman build --clean

*Note:* If you've changed the name of the parent folder, change `slate_app` to the new name in this format `<foldername>_app`. Alternatively, find the exact name of your docker image by running `docker ps`.

#### Dockerfile-Alphine:

    FROM ruby:2.3-alpine
    COPY . /usr/src/app
    VOLUME /usr/src/app
    EXPOSE 4567

    WORKDIR /usr/src/app

    RUN apk add --update nodejs g++ make
    RUN bundle install

    CMD ["bundle", "exec", "middleman", "server", "--watcher-force-polling"]

#### docker-compose.yml :

```yaml
app:
  build: .
  ports:
    - 4567:4567
  volumes:
    - .:/usr/src/app
```
