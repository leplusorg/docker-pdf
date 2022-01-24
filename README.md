# PDF

Docker container to run PDF manipulation utitilies (pdftk, ghostscript...).

[![Docker Build](https://github.com/leplusorg/docker-pdf/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-pdf/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/pdf)](https://hub.docker.com/r/leplusorg/pdf)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/pdf)](https://hub.docker.com/r/leplusorg/pdf)
[![Docker Automated](https://img.shields.io/docker/cloud/automated/leplusorg/pdf)](https://hub.docker.com/r/leplusorg/pdf)
[![Docker Build](https://img.shields.io/docker/cloud/build/leplusorg/pdf)](https://hub.docker.com/r/leplusorg/pdf)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/pdf?sort=semver)](https://hub.docker.com/r/leplusorg/pdf)

## Example not using the filesystem

Assuming that you have a PDF file `foo.pdf` and you want to extract the first page to `bar.pdf`:

**Mac/Linux**

```bash
cat foo.pdf | docker run --rm -i --net=none leplusorg/pdf pdftk - cat output - > bar.pdf 
```

**Windows**

```batch
type foo.pdf | docker run --rm -i --net=none leplusorg/pdf pdftk - cat output - > bar.pdf 
```

## Example requiring the filesystem

Assuming that you have two PDF files `foo.pdf` and `bar.pdf` in your current working directory and you want to join them into a single `foobar.pdf`:

**Mac/Linux**

```bash
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" leplusorg/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

**Windows**

In `cmd`:

```batch
docker run --rm -t --net=none -v "%cd%:/tmp" leplusorg/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

In PowerShell:

```pwsh
docker run --rm -t --net=none -v "${PWD}:/tmp" leplusorg/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

## Help

To know more command-line options of one of the pdftk command:

```bash
docker run --rm --net=none leplusorg/pdf pdftk -h
```

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-pdf/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
