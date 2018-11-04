+++
fragment = "item"
date = "2017-11-04"
weight = 210
background = "light"
align = "left"

subtitle = "Host based redirect using CNAME"

pre = "*www.txtdirect.org*"
post = "*about.txtdirect.org*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen subdomain CNAME to **txtd.io.**
* Create a TXT record with the subdomain **_redirect**
* Use the open TXTDirect spec to configure your redirect

```text
www.txtdirect.org             86000 IN CNAME   txtd.io.
_redirect.www.txtdirect.org   86000 IN TXT     "v=txtv0;to=https://about.txtdirect.org;type=host"
```

## Options
**to=** sets the URL to redirect to  
**code=** can change the redirect code used such as 301 or 302
