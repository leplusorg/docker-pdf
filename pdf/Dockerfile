# Package pdftk requires alpine 3.8.5 or below
FROM alpine:3.8.5

RUN apk --update --no-cache add ghostscript pdftk qpdf \
    && rm -rf /var/cache/apk/*
