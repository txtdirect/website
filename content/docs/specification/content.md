+++
fragment = "content"
weight = 100

title = "Specification"

[sidebar]
  enable = true
  sticky = true
+++

*The specification can be considered stable, but slight changes might happen in the future.*


# General Requirements  

**TXT record**

* Record must not exceed 255 characters
* Record key-value pairs must be delimited by semicolons ";"
* Key and value must be encoded using utf8
* Punycode for domain names should be used
* Ordering key-value pairs can be done
* Arbitrary data/non key-value pairs can be used and will be ignored

**Location/Zone**  

* TXT record must be accessible under the subdomain "_redirect"

**URLs**

* All URLs must be encoded
* ";" must be escaped as "%3B"

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
**Type**  

* Key: **type**
* Mandatory
* Permitted values: "host"
* Example: "type=host"

**Version**  

* Key: **v**
* Mandatory
* Permitted values: "txtv0"
* Example: "v=txtv0"

**Redirect URL**  

* Key: **to**
* Recommended
* Default: Fallback to **www** or **redirect** config
* Permitted values: "absolute|relative URL"
* Example: "to=https://example.com"
* Example: "to=/example/"

**Redirect Code**  

* Key: **code**
* Optional
* Default: "302"
* Permitted values: "301|302"
* Example: "code=301"

---
# Path Type
**Type**  

* Key: **type**
* Mandatory
* Permitted values: "path"
* Example: "type=path"

**Version**  

* Key: **v**
* Mandatory
* Permitted values: "txtv0"
* Example: "v=txtv0"

**Redirect URL**  

* Key: **to**
* Recommended
* Default: Fallback to **www** or **redirect** config
* Permitted values: "absolute|relative URL"
* Example: "to=https://example.com"
* Example: "to=/example/"

**Root Redirect URL**  

* Key: **root**
* Recommended
* Default: Fallback to **www** or **redirect** config
* Permitted values: "absolute|relative URL"
* Example: "to=https://example.com"
* Example: "to=/example/"

**Simplified Regex**  

* Key: **from**
* Permitted values: "simplified regex"
* Example: "from=/$2/$1/$3"

**Regex**  

* Key: **re**
* Permitted values: "regex/ordered regex"
* Note: "Named regexes can be used to reorder the results. a > b > b1 > b2"
* Example: "`from=\\?query=(?P<a>[^&]+)\\&more=(?P<b>[^&]+)`"

---
# Dockerv2 Type
**Type**  

* Key: **type**
* Mandatory
* Permitted values: "dockerv2"
* Example: "type=dockerv2"

**Version**  

* Key: **v**
* Mandatory
* Permitted values: "txtv0"
* Example: "v=txtv0"

**Backend URL**  

* Key: **to**
* Mandatory
* Permitted values: "absolute registry URL"
* Note: "For non container traffic it will fallback to *website*, *www* or *redirect* config"
* Example: "to=https://gcr.io/" *pass through namespaces, container and tag*
* Example: "to=https://gcr.io/txtdirect/container" *pass through tag*
* Example: "to=https://gcr.io/txtdirect/container:tag" *force specific tag*

**Website Redirect URL**  

* Key: **website**
* Recommended
* Default: Fallback to **www** or **redirect** config
* Note: "Non container traffic redirect"
* Permitted values: "absolute|relative URL"
* Example: "to=https://about.txtdirect.org/docs/"
* Example: "to=/docs/"

---
# Gometa Type
**Type**  

* Key: **type**
* Mandatory
* Permitted values: "gometa"
* Example: "type=gometa"

**Version**  

* Key: **v**
* Mandatory
* Permitted values: "txtv0"
* Example: "v=txtv0"

**Backend URL**  

* Key: **to**
* Recommended
* Default: Fallbacks such as **www** or **redirect** config
<!--* Note: "For non container traffic it will fallback to *website*, *www* or *redirect* config"-->
* Permitted values: "absolute repository URL"
* Example: "to=https://github.com/txtdirect/"
* Example: "to=/docs/"

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

* Key: **vcs**
* Recommended
* Default: **git**
* Permitted values: "git|bzr|fossil|hg|svn"
* Example: "to=https://github.com/txtdirect/"


---
# Proxy Type (experimental)
**Type**  

* Key: **type**
* Mandatory
* Permitted values: "proxy"
* Example: "type=proxy"

**Version**  

* Key: **v**
* Mandatory
* Permitted values: "txtv0"
* Example: "v=txtv0"

**Upstream URL**  

* Key: **to**
* Mandatory
* Permitted values: "absolute URL"
* Example: "to=https://example.com/subpage/"
<!--root/website?-->

---
# Tor Type (experimental)
**Type**  

* Key: **type**
* Mandatory
* Permitted values: "tor"
* Example: "type=tor"

**Version**  

* Key: **v**
* Mandatory
* Permitted values: "txtv0"
* Example: "v=txtv0"

**Upstream URL**  

* Key: **to**
* Mandatory
* Permitted values: "absolute URL"
* Example: "to=http://3g2upl4pq6kufc4m.onion/"

<!--root/website?-->