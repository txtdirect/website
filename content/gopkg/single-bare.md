+++
fragment = "item"
#disabled = false
date = "2017-11-04"
weight = 320
background = "dark"
align = "left"

title = """
Single repository import  
(bare domain)
"""

icon = "fas fa-arrow-down"

pre = "*example.com*"
post = "*github.com/txtdirect/txtdirect*"

+++

* Point your chosen root by A-record to `35.201.81.193`
* Point your chosen root by AAAA-record to `2600:1901:0:3f61:0:0:0:0`
* Create a TXT record with the subdomain `_redirect` for your domain
* Use the open TXTDirect spec to set your specific repository

```text
example.com             86000 IN A       35.201.81.193
example.com             86000 IN AAAA    2600:1901:0:3f61:0:0:0:0
_redirect.example.com   86000 IN TXT     "v=txtv0;to=https://github.com/txtdirect/txtdirect;type=gometa"
```
