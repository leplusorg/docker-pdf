# PDF

Docker container to run PDF manipulation utitilies (pdftk, ghostscript...).

## Example

Assuming that you have two PDF files `foo.pdf` and `bar.pdf` in your current working directory and you want to join them into a single `foobar.pdf`:

### Mac/Linux

```
$ docker run --rm -it --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" thomasleplus/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

### Windows

In `cmd`:

```
$ docker run --rm -it --net=none -v "%cd%:/tmp" thomasleplus/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

In PowerShell:

```
$ docker run --rm -it --net=none -v "${PWD}:/tmp" thomasleplus/pdf pdftk /tmp/foo.pdf /tmp/bar.pdf cat output /tmp/foobar.pdf
```

## Help

To know more command line options of one of the pdftk command:

```
$ docker run --rm -it --net=none thomasleplus/pdf pdftk -h
```
