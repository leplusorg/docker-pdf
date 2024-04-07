# Package pdftk requires alpine 3.8.5 or below
FROM alpine:3.8.5@sha256:2bb501e6173d9d006e56de5bce2720eb06396803300fe1687b58a7ff32bf4c14

# hadolint ignore=DL3018
RUN apk --update --no-cache add \
    ghostscript \
    ocrmypdf \
    pdfgrep \
    pdftk \
    qpdf \
    && rm -rf /var/cache/apk/*
