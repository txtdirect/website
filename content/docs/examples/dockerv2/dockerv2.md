+++
fragment = "content"
disabled = false
weight = 300

title = "Dockerv2"

[sidebar]
  enable = true
+++

**Currently Docker hub is not supported**
**Only publicly available containers are currently supported**

# Dockerv2

**Container vanity redirect**  
_container.example.com/txtdirect -> gcr.io/some/container_
_container.example.com/txtdirect:tag -> gcr.io/some/container:tag_

```
container.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.container.example.com   3600 IN TXT    "v=txtv0;type=dockerv2;to=https://gcr.io/some/container"
```

**Container vanity redirect with enforced tag**  
_container.example.com/txtdirect -> gcr.io/some/container:tag_  
_container.example.com/txtdirect:123 -> gcr.io/some/container:tag_

```
container.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.container.example.com   3600 IN TXT    "v=txtv0;type=dockerv2;to=https://gcr.io/some/container:tag"
```

**Full platform container vanity redirects**  
_gcr.example.com/some/container -> gcr.io/some/container_  
_gcr.example.com/some/container:tag -> gcr.io/some/container:tag_  
\*gcr.example.com/\* -> gcr.io/\*\*

```
gcr.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.gcr.example.com   3600 IN TXT    "v=txtv0;type=dockerv2;to=https://gcr.io"
```
