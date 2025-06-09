# PDF

Docker container with utilities to process PDF (pdftk, ghostscript, ocrmypdf, pdfgrep, qpdf...).

[![Dockerfile](https://img.shields.io/badge/GitHub-Dockerfile-blue)](pdf/Dockerfile)
[![Docker Build](https://github.com/leplusorg/docker-pdf/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-pdf/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/pdf)](https://hub.docker.com/r/leplusorg/pdf)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/pdf)](https://hub.docker.com/r/leplusorg/pdf)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/pdf?sort=semver)](https://hub.docker.com/r/leplusorg/pdf)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/10072/badge)](https://bestpractices.coreinfrastructure.org/projects/10072)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/leplusorg/docker-pdf/badge)](https://securityscorecards.dev/viewer/?uri=github.com/leplusorg/docker-pdf)

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

## Software Bill of Materials (SBOM)

To get the SBOM for the latest image (in SPDX JSON format), use the
following command:

```bash
docker buildx imagetools inspect leplusorg/pdf --format '{{ json (index .SBOM "linux/amd64").SPDX }}'
```

Replace `linux/amd64` by the desired platform (`linux/amd64`, `linux/arm64` etc.).

### Sigstore

[Sigstore](https://docs.sigstore.dev) is trying to improve supply
chain security by allowing you to verify the origin of an
artifcat. You can verify that the jar that you use was actually
produced by this repository. This means that if you verify the
signature of the ristretto jar, you can trust the integrity of the
whole supply chain from code source, to CI/CD build, to distribution
on Maven Central or whever you got the jar from.

You can use the following command to verify the latest image using its
sigstore signature attestation:

```bash
cosign verify leplusorg/pdf --certificate-identity-regexp 'https://github\.com/leplusorg/docker-pdf/\.github/workflows/.+' --certificate-oidc-issuer 'https://token.actions.githubusercontent.com'
```

The output should look something like this:

```text
Verification for index.docker.io/leplusorg/xml:main --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates

[{"critical":...
```

For instructions on how to install `cosign`, please read this [documentation](https://docs.sigstore.dev/cosign/system_config/installation/).

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-pdf/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
