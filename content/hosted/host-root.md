+++
fragment = "item"
date = "2017-11-04"
weight = 220
background = "white"
align = "left"

subtitle = "Host based redirect on root record"

pre = "*txtdirect.org*"
post = "*about.txtdirect.org*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen root A-record to **35.201.95.240**
* Point your chosen root AAAA-record to **2600:1901:0:cdc7:0:0:0:0**
* Create a TXT record with the subdomain **_redirect**
* Use the open TXTDirect spec to configure your redirect

```text
txtdirect.org             86000 IN A       35.201.95.240
txtdirect.org             86000 IN AAAA    2600:1901:0:cdc7:0:0:0:0
_redirect.txtdirect.org   86000 IN TXT     "v=txtv0;to=https://about.txtdirect.org;type=host"
```

## Options
**to=** sets the URL to redirect to  
**code=** can change the redirect code used such as 301 or 302
