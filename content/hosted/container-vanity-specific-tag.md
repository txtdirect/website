+++
fragment = "item"
date = "2018-09-08"
weight = 420
background = "light"
align = "left"

subtitle = "Container vanity url for a specific tag"

pre = "*c.txtdirect.org/txtdirect*"
post = "*gcr.io/txtdirect-223710/txtdirect:dev-3fd9be*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen subdomain CNAME to **txtd.io.**
* Create a TXT record with the subdomain **_redirect**
* Use the open TXTDirect spec to configure your vanity url

```text
c.txtdirect.org                    86000 IN CNAME   txtd.io.
_redirect.c.txtdirect.org          86400 IN TXT     "v=txtv0;to=https://gcr.io/txtdirect-223710/txtdirect:dev-3fd9be;type=dockerv2"
```

### Options
**to=** sets the backend URL for the registry/container  
**website=** (non container traffic) sets the general fallback URL  
**root=** (non container traffic) sets the fallback URL, when the root path is requested
