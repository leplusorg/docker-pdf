# Package pdftk requires alpone 3.8 or below
FROM alpine:3.8

RUN apk --update --no-cache add ghostscript pdftk qpdf \
    && rm -rf /var/cache/apk/*
