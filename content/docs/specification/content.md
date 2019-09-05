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

`host` is the most simple type. Using `host` you can redirect an incoming request to a specific endpoint with a custom status code defined in the TXT record.
For example records you can check [host](https://about.txtdirect.org/docs/examples/#host).

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

Sometimes you may need to redirect a request coming into a single host/domain to separate locations based on the request's path. One common use-case is a URL shortener.
`path` type extracts each directory by default. Each directory is used to generate a new sub zone to fetch the TXT record from. To reorder the default order you can use the `from=` field.

`path` also contains some additional configuration to process the request's path. The `re=` field enables use of a custom regex to control which data is used to construct the sub zones, where TXT record data is fetched.

### Path Sanitization

To use the request's path for generating the zone address it needs to be normalized into allowed DNS chars. For example `.`(dot) is replaced with `-`(dash) to keep each match in its own zone. You can visit [RFC1034](https://tools.ietf.org/html/rfc1034) for more information about the allowed chars.

The request's path is used to construct the zone address, which provides the redirect data used for this specific path. By default each directory is extracted and the order reverted meaning the less specific zone will come first:
`example.com/firstDirectory/secondDirectory/ -> secondDirectory.firstDirectory.example.com`
A custom ordering can be achieved by using the `from=` field. It will reorder the sub zones accordingly.
If a custom regex is configured with the `re=` field each match is used as a sub zone. Ordering can be modified by using named matches. The default ordering will use the first match as the first sub zone and continue until there are no new matches.

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
- Example: "from=/$2/$1/$3"

**Regex**

- Key: **re**
- Permitted values: "regex/ordered regex"
- Note: "Named regexes can be used to reorder the results. a > b > b1 > b2"
- Example: "`re=\\?query=(?P<a>[^&]+)\\&more=(?P<b>[^&]+)`"

---

# Dockerv2 Type

## Description

The `dockerv2` type enables vanity URLs for your container images. Using your own URl for container images enables easier switching between your backend infrastructure/storage and adds more control.
The type implements the Docker registry API v2 and redirects requests for both metadata and image blobs to the backend storage. All data besides the redirect is therefore served by your underlying infrastructure such as Google Container Registry (gcr.io).

The upstream endpoint used for `to=` can be different depending on the use case.

1. Image link including a specific tag enables serving this specific tag under various image names and tags.
2. Image link enables serving available tags for a specific image under various image names.
3. Referencing the root of a container registry enables the full serving of the registry under this specific domain.

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

---

# Gometa Type

## Description

The `gometa` type enables vanity URLs for your Go packages. Using your own URL for packages, enables easier switching between your backend hosting service (GitHub, etc.) and lets you have custom import path for your package, independent of your hosting service. Using `gometa` you can switch your hosting service without worrying about impacting downstream for your users.
Using `gometa` type you can point to a Go package inside your records using the `to=` field and we use that URI to generate a simple HTML page that only contains go-import and go-source **(Only for packages served on GitHub)** tags for `go get` to use it and find your package.

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

# Gomods Type

## Description

The `gomods` type provides vanity urls for Go modules. It uses the request's path to identify a Go package's import path. Then it fetches the package and module files like `info`, `mod` and `zip` to serve a `go get` request. `gomods` supports all the hosting services and VCS` that are supported by Go tools.

It also provides local caching for Go modules. You can also define a custom Go binary for fetching the modules and a custom number of workers for the module downloader's stash.

The `gomods` type doesn't require any specific config in the DNS records and gets configured in the [TXTDirect config](/docs/configuration#gomods-config).

**Type**

- Key: **type**
- Mandatory
- Permitted values: "gomods"
- Example: "type=gomods"

**Version**

- Key: **v**
- Mandatory
- Permitted values: "txtv0"
- Example: "v=txtv0"

---

# Proxy Type (experimental)

## Description

The `proxy` type let's you proxy your requests to a specific upstream. It reads the upstream from the record's `to=` field and reverse proxies the request.

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
