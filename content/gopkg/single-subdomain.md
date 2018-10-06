+++
fragment = "item"
#disabled = false
date = "2017-11-04"
weight = 310
background = "secondary"
align = "left"

title = "Single repository import"

pre = "*pkg.txtdirect.org*"
post = "*github.com/txtdirect/txtdirect*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen subdomain by CNAME to `gopkg.link.`
* Create a TXT record with the subdomain `_redirect` for your subdomain
* Use the open TXTDirect spec to set your specific repository

```text
pkg.txtdirect.org             86000 IN CNAME   gopkg.link.
_redirect.org.txtdirect.org   86000 IN TXT     "v=txtv0;to=https://github.com/txtdirect/txtdirect;type=gometa"
```
