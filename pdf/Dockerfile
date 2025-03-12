FROM alpine:3.21.3@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# hadolint ignore=DL3018
RUN apk --update --no-cache add \
    curl \
    ghostscript \
    jq \
    ocrmypdf \
    openjdk21-jre-headless \
    pdfgrep \
    qpdf \
    && rm -rf /var/cache/apk/*

RUN VERSION=$(curl -s -S -f https://gitlab.com/api/v4/projects/5024297/releases | jq -r '.[0].tag_name') \
    && mkdir -p /opt/pdftk/lib \
    && curl -s -S -f -o /opt/pdftk/lib/pdftk-all.jar \
    "https://gitlab.com/api/v4/projects/5024297/packages/generic/pdftk-java/${VERSION}/pdftk-all.jar"

COPY pdftk /usr/bin/pdftk

RUN chmod 755 /usr/bin/pdftk

RUN adduser \
  --home "${USER_HOME}" \
  --uid "${USER_ID}" \
  --gecos "${USER_GECOS}" \
  --disabled-password \
  "${USER_NAME}"

ENV HOME="${USER_HOME}"

USER "${USER_NAME}"

WORKDIR "${HOME}"
