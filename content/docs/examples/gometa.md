+++
fragment = "content"
weight = 400

title = "Gometa"

[sidebar]
  enable = true
+++

## Gometa
**Go package vanity redirect**
*pkg.example.com -> github.com/some/repo*
```
pkg.example.com               3600 IN CNAME  txtdirect.example.com.
_redirect.pkg.example.com     3600 IN TXT    "v=txtv0;type=gometa;to=https://github.com/some/repo"
```
