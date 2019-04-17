+++
fragment = "content"
weight = 100

title = "Specification"

[sidebar]
  enable = true
  sticky = true
+++

_The specification can be considered stable, but slight changes might happen in the future._

# General Requirements

**TXT record**

- Record must not exceed 255 characters
- Record key-value pairs must be delimited by semicolons ";"
- Key and value must be encoded using utf8
- Punycode for domain names should be used
- Ordering key-value pairs can be done
- Arbitrary data/non key-value pairs can be used and will be ignored

**Location/Zone**

- TXT record must be accessible under the subdomain "\_redirect"

**URLs**

- All URLs must be encoded
- ";" must be escaped as "%3B"

Examples:

```; -> %3B
? -> %3F
= -> %3D
https://example.com/page/about=us -> https://example.com/page/about%3Dus
```

Further links about URL encoding:  
https://en.wikipedia.org/wiki/Percent-encoding  
https://tools.ietf.org/html/rfc3986#page-11

---

# Host Type

## Description

`host` is our most simple type. Using `host` you can redirect an incoming request to a specific endpoint with a custom status code defined in the TXT record.
For example records you can check [host](https://about.txtdirect.org/docs/examples/#host) in the examples section.

## Record fields

**Type**

- Key: **type**
- Mandatory
- Permitted values: "host"
- Example: "type=host"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

**Redirect URL**

- Key: **to**
- Recommended
- Default: Fallback to **www** or **redirect** config
- Permitted values: "absolute|relative URL"
- Example: "to=https://example.com"
- Example: "to=/example/"

**Redirect Code**

- Key: **code**
- Optional
- Default: "302"
- Permitted values: "301|302"
- Example: "code=301"

---

# Path Type

## Description

Sometimes you may need to redirect a request separate endpoints based on the request's path content. `path` type runs a regular expression which can be our default regex or a custom regex from the TXT record. Then uses the matches from that expression to generate a zone address and find final record to use it for redirecting the request.

`path` also contains some additional configuration to process the request's path. For example by using `from=` field inside a `path` record you can define how we should order the matches from the expression on the request's path to generate the next zone address. Or add the `re=` field to use a custom regex instead of our default on the request's path.

### Path Sanitization

To use the request's path for generating the zone address we need normalize the path into allowed DNS chars. For example we need to replace `.`(dot) into `-`(dash) to keep each match in its own zone. You can visit [RFC1034](https://tools.ietf.org/html/rfc1034) for more information about the allowed chars.

After this step we run our default regex or the custom regex from `re=` field on the request's path. If `from=` is not available we first revert order of matches from the expression then join them with request's host to generate the next zone in the chain. But if `from=` is availabe, we use the given order instead of reverting.

## Record Fields

**Type**

- Key: **type**
- Mandatory
- Permitted values: "path"
- Example: "type=path"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

**Redirect URL**

- Key: **to**
- Recommended
- Default: Fallback to **www** or **redirect** config
- Permitted values: "absolute|relative URL"
- Example: "to=https://example.com"
- Example: "to=/example/"

**Root Redirect URL**

- Key: **root**
- Recommended
- Default: Fallback to **www** or **redirect** config
- Permitted values: "absolute|relative URL"
- Example: "to=https://example.com"
- Example: "to=/example/"

**Simplified Regex**

- Key: **from**
- Permitted values: "simplified regex"
- Example: "from=/$2/$1/\$3"

**Regex**

- Key: **re**
- Permitted values: "regex/ordered regex"
- Note: "Named regexes can be used to reorder the results. a > b > b1 > b2"
- Example: "`from=\\?query=(?P<a>[^&]+)\\&more=(?P<b>[^&]+)`"

---

# Dockerv2 Type

## Description

To redirect request from Docker CLI to a specific docker image or a docker registry you can use `dockerv2` type. The difference between a Docker CLI request and a normal request is that Docker CLI sends a couple of request with different paths to fetch some information like image tags, manifests and etc. about the image. To handle these requests we use docker's v2 API to fetch the data for each request.

You can point to a docker registry or a specific image inside your record. With pointing to a registry you can have vanity urls for all the images on that registry instead of only an image.

## Record Fields

**Type**

- Key: **type**
- Mandatory
- Permitted values: "dockerv2"
- Example: "type=dockerv2"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

**Backend URL**

- Key: **to**
- Mandatory
- Permitted values: "absolute registry URL"
- Note: "For non container traffic it will fallback to _website_, _www_ or _redirect_ config"
- Example: "to=https://gcr.io/" _pass through namespaces, container and tag_
- Example: "to=https://gcr.io/txtdirect/container" _pass through tag_
- Example: "to=https://gcr.io/txtdirect/container:tag" _force specific tag_

**Website Redirect URL**

- Key: **website**
- Recommended
- Default: Fallback to **www** or **redirect** config
- Note: "Non container traffic redirect"
- Permitted values: "absolute|relative URL"
- Example: "to=https://about.txtdirect.org/docs/"
- Example: "to=/docs/"

---

# Gometa Type

## Description

One of the features that `go get` command has is that you can point a webpage to a Go package using go-import meta tag. For more information about these tags please visit [Remote import paths](https://golang.org/cmd/go/#hdr-Remote_import_paths). Using `gometa` type you can point to a go package inside your records using `to=` field and we use that URI to generate a simple HTML page that only contains go-import and go-source **(Only for packages served on GitHub)** tags for `go get` to use it and find your package.

## Record fields

**Type**

- Key: **type**
- Mandatory
- Permitted values: "gometa"
- Example: "type=gometa"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

**Backend URL**

- Key: **to**
- Recommended
- Default: Fallbacks such as **www** or **redirect** config
  <!--* Note: "For non container traffic it will fallback to *website*, *www* or *redirect* config"-->
- Permitted values: "absolute repository URL"
- Example: "to=https://github.com/txtdirect/"
- Example: "to=/docs/"

<!--
**Website Redirect URL**

* Key: **website**
* Recommended
* Default: Fallback to **www** or **redirect** config
* Note: "Non gometa traffic redirect"
* Permitted values: "absolute|relative URL"
* Example: "to=https://about.txtdirect.org/docs/"
* Example: "to=/docs/"
-->

**Repository Type**

- Key: **vcs**
- Recommended
- Default: **git**
- Permitted values: "git|bzr|fossil|hg|svn"
- Example: "to=https://github.com/txtdirect/"

---

# Proxy Type (experimental)

**Type**

- Key: **type**
- Mandatory
- Permitted values: "proxy"
- Example: "type=proxy"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

**Upstream URL**

- Key: **to**
- Mandatory
- Permitted values: "absolute URL"
- Example: "to=https://example.com/subpage/"
  <!--root/website?-->

---

# Tor Type (experimental)

**Type**

- Key: **type**
- Mandatory
- Permitted values: "tor"
- Example: "type=tor"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

**Upstream URL**

- Key: **to**
- Mandatory
- Permitted values: "absolute URL"
- Example: "to=http://3g2upl4pq6kufc4m.onion/"

<!--root/website?-->
