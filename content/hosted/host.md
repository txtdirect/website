+++
fragment = "item"
#disabled = false
date = "2017-11-04"
weight = 210
background = "light"
align = "left"

subtitle = "Host based redirect using CNAME"

icon = "fas fa-arrow-down"

pre = "*www.txtdirect.org*"
post = "*about.txtdirect.org*"
+++

* Point your chosen subdomain by CNAME to `txtdirect.io.`
* Create a TXT record with the subdomain `_redirect`
* Use the open TXTDirect spec to set your specific repository

```text
www.txtdirect.org             86000 IN CNAME   txtdirect.io.
_redirect.www.txtdirect.org   86000 IN TXT     "v=txtv0;to=https://about.txtdirect.org;type=host"
```

## Options
`to=` sets the URL to redirect to  
`code=` can change the redirect code used such as 301 or 302
