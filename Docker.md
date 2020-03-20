Some people have had success with Docker, although it is not officially supported. You'll need to create three files in your Slate directory:

## Ruby 2.6.5

#### .dockerignore :

    .git
    source

#### Dockerfile :

```dockerfile
FROM ruby:2.6.5

RUN apt-get update && apt-get install -y nodejs \
&& apt-get clean && rm -rf /var/lib/apt/lists/*

COPY ./Gemfile /usr/src/app/
COPY ./Gemfile.lock /usr/src/app/
WORKDIR /usr/src/app

RUN gem install bundler --version '2.0.2'
RUN bundle install

COPY . /usr/src/app
VOLUME /usr/src/app/source

EXPOSE 4567

CMD ["bundle", "exec", "middleman", "server", "--watcher-force-polling"]
```

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

    docker run --rm -v $PWD/source:/usr/src/app/source -w /usr/src/app/source -v $PWD/build:/usr/src/app/build slate_app bundle exec middleman build --clean

*Note:* If you've changed the name of the parent folder, change `slate_app` to the new name in this format `<foldername>_app`. 

Alternatively, find the exact name of your docker image by running `docker images | grep _app`.

## Ruby 2.3 Alpine

#### Dockerfile-Alpine:

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

## Alternative approach with Ruby 2.5 Alpine

From: https://github.com/cashlink/apidoc

In this setup we don't clone the slate repository and make our changes directly in its `source` directory. Instead we have a separate source directory somewhere in our app's repository, let's call it `doc-source`. The slate repository lives only in the Docker image. Files in `doc-source` overwrite the files in the slate `source` directory.

#### Dockerfile

```docker
FROM ruby:2.5-alpine
EXPOSE 4567

RUN apk update \
 && apk add coreutils git make g++ nodejs

RUN git clone https://github.com/slatedocs/slate /slate/source_orig

RUN cd /slate/source_orig && bundle install

VOLUME /slate/source
VOLUME /slate/build

CMD cd /slate && cp -nr source_orig/* source && cd source && exec bundle exec middleman server --watcher-force-polling
```

#### doc-source/.gitignore

```
fonts
images
includes
javascripts
layouts
stylesheets
```

Note that you will have to use `git add -f` if you want to add overwrite e.g. `images/logo.png`.

#### Run server

```
docker run -p 4567:4567 -v /path/to/doc-source:/slate/source -v /path/to/build:/slate/build <image>
```

#### Build

```
docker run -v /path/to/doc-source:/slate/source -v /path/to/build:/slate/build <image> \
  sh -c 'cd /slate && cp -nr source_orig/* source && exec bundle exec middleman build'
```

This will build the site into the `/path/to/build` directory.