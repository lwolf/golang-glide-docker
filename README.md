# golang-glide-builder

Pure golang alpine image with glide installed


# Usage

Dockerfile:

```
FROM lwolf/golang-glide-builder


# replace <YOUR-PACKAGE-NAME> with something like github.com/user/app
ENV APP_PATH=/go/src/<YOUR-PACKAGE-NAME>

RUN mkdir -p $APP_PATH
WORKDIR $APP_PATH

COPY glide.yaml glide.yaml
COPY glide.lock glide.lock

RUN glide install -v

VOLUME ["/build"]

ADD . $APP_PATH
CMD CGO_ENABLED=0 go build -o /build/app

```