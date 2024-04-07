# Package pdftk requires alpine 3.8.5 or below
FROM alpine:3.8.5

# hadolint ignore=DL3018
RUN apk --update --no-cache add \
    ghostscript \
    ocrmypdf \
    pdfgrep \
    pdftk \
    qpdf \
    && rm -rf /var/cache/apk/*
