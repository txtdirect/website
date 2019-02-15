+++
fragment = "content"
disabled = false
weight = 300

title = "Dockerv2"

[sidebar]
  enable = true
+++

__Currently Docker hub is not supported__
__Only publicly available containers are currently supported__

## Dockerv2
**Container vanity redirect**  
*container.example.com/txtdirect -> gcr.io/some/container*
*container.example.com/txtdirect:tag -> gcr.io/some/container:tag*
```
container.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.container.example.com   3600 IN TXT    "v=txtv0;to=https://gcr.io/some/container;type=dockerv2"
```

**Container vanity redirect with enforced tag**  
*container.example.com/txtdirect -> gcr.io/some/container:tag*  
*container.example.com/txtdirect:123 -> gcr.io/some/container:tag*
```
container.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.container.example.com   3600 IN TXT    "v=txtv0;to=https://gcr.io/some/container:tag;type=dockerv2"
```

**Full platform container vanity redirects**  
*gcr.example.com/some/container -> gcr.io/some/container*  
*gcr.example.com/some/container:tag -> gcr.io/some/container:tag*  
*gcr.example.com/\* -> gcr.io/\**
```
gcr.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.gcr.example.com   3600 IN TXT    "v=txtv0;to=https://gcr.io;type=dockerv2"
```
