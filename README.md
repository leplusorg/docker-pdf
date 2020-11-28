# PDF

Docker container to run PDF manipulation utitilies (pdftk, ghostscript...).

![Docker Build](https://github.com/thomasleplus/docker-pdf/workflows/Docker/badge.svg)
![Docker Stars](https://img.shields.io/docker/stars/thomasleplus/pdf)
![Docker Pulls](https://img.shields.io/docker/pulls/thomasleplus/pdf)
![Docker Automated](https://img.shields.io/docker/cloud/automated/thomasleplus/pdf)
![Docker Build](https://img.shields.io/docker/cloud/build/thomasleplus/pdf)
![Docker Version](https://img.shields.io/docker/v/thomasleplus/pdf?sort=semver)

## Example not using the filesystem

Assuming that you have a PDF file `foo.pdf` and you want to extract the first page to `bar.pdf`:

### Mac/Linux

```
cat foo.pdf | docker run --rm -i --net=none thomasleplus/pdf pdftk - cat output - > bar.pdf 
```

### Windows

```
type foo.pdf | docker run --rm -i --net=none thomasleplus/pdf pdftk - cat output - > bar.pdf 
```

## Example requiring the filesystem

Assuming that you have two PDF files `foo.pdf` and `bar.pdf` in your current working directory and you want to join them into a single `foobar.pdf`:

### Mac/Linux

```
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" thomasleplus/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

### Windows

In `cmd`:

```
docker run --rm -t --net=none -v "%cd%:/tmp" thomasleplus/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

In PowerShell:

```
docker run --rm -t --net=none -v "${PWD}:/tmp" thomasleplus/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

## Help

To know more command line options of one of the pdftk command:

```
docker run --rm --net=none thomasleplus/pdf pdftk -h
```

## Request new tool

Please use [this link](https://github.com/thomasleplus/docker-pdf/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
