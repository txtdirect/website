+++
fragment = "content"
weight = 100

title = "Getting Started"

[sidebar]
  enable = true
  sticky = true
+++

# Introduction

TXTDirect is a tool that provides convenient and minimalistic DNS based redirects, while controlling your data with your own DNS records. Using TXTDirect you can have vanity urls for your Go packages and Docker images, configure TXT records to proxy or redirect your requests to a specific endpoint and lots of more features to discover.

# Usage and Installation

There are two ways to install TXTDirect. You can either fetch and compile the package using `go get` command or use the Docker image.

## Install with `go get`

Use the following command to fetch the package using go tools.

```
$ go get go.txtdirect.org/txtdirect
```

After running the command, you can find the binary file in your `$GOPATH/bin` directory.

## Install with Docker

You can check the list of available Docker images on [c.txtdirect.org/txtdirect](https://c.txtdirect.org/txtdirect)

Use the following command with the version of your choice:

```
$ docker pull c.txtdirect.org/txtdirect:v0.4.0
```

## Run TXTDirect

To run an instance of TXTDirect you have to write an configuration file and give it to the TXTDirect binary or container. More details about the types and their configurations are available in the [Configuration](/docs/configuration) page.

Run an TXTDirect instance using the following command:

```
$ txtdirect -conf CONFIG_FILE
```

CONFIG_FILE is the path to your config file.
