FROM alpine:3.23.0@sha256:51183f2cfa6320055da30872f211093f9ff1d3cf06f39a0bdb212314c5dc7375

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-euo", "pipefail", "-c"]

RUN apk upgrade --no-cache \
    && apk add --no-cache \
    coreutils=9.8-r1 \
    curl=8.17.0-r1 \
    ghostscript=10.06.0-r0 \
    git=2.52.0-r0 \
    jq=1.8.1-r0 \
    libreoffice=25.8.1.1-r5 \
    openjdk21-jre-headless=21.0.10_p7-r0 \
    pandoc-cli=3.8.2.1-r0 \
    pdfgrep=2.2.0-r1 \
    pipx=1.8.0-r0 \
    poppler-utils=25.12.0-r0 \
    py3-pip=25.1.1-r1 \
    python3=3.12.12-r0 \
    qpdf=12.2.0-r0 \
    && apk cache --no-cache clean \
    && rm -rf /var/cache/apk/*

COPY requirements.txt /tmp/requirements.txt

RUN pipx ensurepath --global \
    && xargs -a /tmp/requirements.txt -n 1 pipx install --global \
    && rm -f /tmp/requirements.txt

RUN VERSION=$(curl -s -S -f https://gitlab.com/api/v4/projects/5024297/releases | jq -r '.[0].tag_name') \
    && mkdir -p /opt/pdftk/lib \
    && curl -s -S -f -o /opt/pdftk/lib/pdftk-all.jar \
    "https://gitlab.com/api/v4/projects/5024297/packages/generic/pdftk-java/${VERSION}/pdftk-all.jar" \
    && chmod -R o+rX /opt/pdftk

COPY pdftk /usr/bin/pdftk

RUN chmod 755 /usr/bin/pdftk

RUN adduser \
  --home "${USER_HOME}" \
  --uid "${USER_ID}" \
  --gecos "${USER_GECOS}" \
  --disabled-password \
  "${USER_NAME}"

USER "${USER_NAME}"

ENV HOME="${USER_HOME}"

WORKDIR "${HOME}"
