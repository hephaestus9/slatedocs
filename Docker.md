Some people have had success with Docker, although it is not officially supported. You'll need to create three files in your Slate directory:

`.dockerignore`

    .git
    source

`Dockerfile`

    FROM ruby:onbuild
    MAINTAINER Adrian Perez <adrian@adrianperez.org>
    VOLUME /usr/src/app/source
    EXPOSE 4567

    RUN apt-get update && apt-get install -y nodejs \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

    CMD ["bundle", "exec", "middleman", "server", "--force-polling"]

`docker-compose.yml`

    app:
      build: .
      ports:
        - 4567:4567
      volumes:
        - ./source:/usr/src/app/source

After the files have been created, you can run Slate with `docker-compose up`.