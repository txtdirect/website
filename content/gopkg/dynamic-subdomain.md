+++
fragment = "item"
disabled = true
date = "2017-11-04"
weight = 340
background = "secondary"
align = "left"

title = "Dynamic subdomain import"

icon = "fas fa-arrow-down"

pre = "*pkg.txtdirect.org/caddy*"
post = "*github.com/txtdirect/txtdirect/caddy*"

+++

* Point your chosen subdomain by CNAME to `gopkg.link.`
* Create a TXT record with the subdomain `_redirect` for your subdomain
* Use the open TXTDirect spec to set your specific repository

```text
pkg.txtdirect.org                   86000 IN CNAME   gopkg.link.
_redirect.pkg.txtdirect.org         86000 IN TXT     "v=txtv0;to=/$1;type=gometa-path"
_redirect.caddy.pkg.txtdirect.org   86000 IN TXT     "v=txtv0;to=https://github.com/txtdirect/txtdirect/caddy;type=gometa"
```

Full documentation on how to use dynamic imports including the supported simplified and full regex available can be accessed
