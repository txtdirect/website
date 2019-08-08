+++
fragment = "item"
date = "2017-11-04"
weight = 220
background = "white"
align = "left"

subtitle = "Host redirect on root record"

pre = "*txtdirect.org*"
post = "*about.txtdirect.org*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen root A-record to **45.85.238.5**
* Point your chosen root AAAA-record to **2a0e:c885:5::1**
* Create a TXT record with the subdomain **_redirect**
* Use the open TXTDirect spec to configure your redirect

```text
txtdirect.org             86000 IN A       45.85.238.5
txtdirect.org             86000 IN AAAA    2a0e:c885:5::1
_redirect.txtdirect.org   86000 IN TXT     "v=txtv0;to=https://about.txtdirect.org;type=host"
```

### Options
**to=** sets the URL to redirect to  
**code=** can change the redirect code used such as 301 or 302  
