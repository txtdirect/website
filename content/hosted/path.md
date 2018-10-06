+++
fragment = "item"
#disabled = false
date = "2018-09-08"
weight = 310
background = "light"
align = "left"

subtitle = "Path based redirect"

pre = "*s.txtdirect.org/hosted*"
post = "*about.txtdirect.org/hosted*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen subdomain by CNAME to `txtdirect.io.`
* Create a TXT record with the subdomain `_redirect`
* Use the open TXTDirect spec to set your specific repository

```text
www.txtdirect.org                  86000 IN CNAME   txtdirect.io.
_redirect.s.txtdirect.org          86400 IN TXT     "v=txtv0;to=https://about.txtdirect.org;root=https://about.txtdirect.org;type=path"
_redirect.hosted.s.txtdirect.org   86400 IN TXT     "v=txtv0;to=https://about.txtdirect.org/hosted;type=host;code=302"
```

## Default lookup
The path type defaults to looking up each path as subdomain.
Requesting a domain such as example.com/firstMatch/secondMatch would lookup `_redirect.secondmatch.firstmatch.example.com`.
If no specific subdomain is found, it will try to fallback to wildcard. Wildcards will iterate from first subdomain to last.

The lookup order would look like this:
```
_redirect.secondmatch.firstmatch.example.com
_redirect._.firstmatch.example.com
_redirect._._.example.com
```

## Options
### Within path type
`to=` sets the URL to fallback to, if no specific path subdomain is matched
`root=` sets the URL redirect to, when the root path is requested

### Within host type
`to=` sets the URL to redirect to
`code=` can change the redirect code used such as 301 or 302
