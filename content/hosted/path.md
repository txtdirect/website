+++
fragment = "item"
date = "2018-09-08"
weight = 310
background = "white"
align = "left"

subtitle = "Path based redirect (shortener)"

pre = "*s.txtdirect.org/hosted*"
post = "*about.txtdirect.org/hosted*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen subdomain CNAME to **txtd.io.**
* Create a TXT record with the subdomain **_redirect**
* Use the open TXTDirect spec to configure your redirect

```text
s.txtdirect.org                    86000 IN CNAME   txtd.io.
_redirect.s.txtdirect.org          86400 IN TXT     "v=txtv0;to=https://about.txtdirect.org;root=https://about.txtdirect.org;type=path"

_redirect.hosted.s.txtdirect.org   86400 IN TXT     "v=txtv0;to=https://about.txtdirect.org/hosted;type=host;code=302"
```

Path redirect uses two different types.  
The **path** record configures an endpoint to use path based routing.
Specific **host** records are then used for the redirects.

By default requesting example.com/firstMatch/secondMatch looks up **_redirect.secondmatch.firstmatch.example.com**.

In the case a specific record is not provided it will use wildcards.  
Ordered from most specific to least specific such as:
```
_redirect.secondmatch.firstmatch.example.com
_redirect._.firstmatch.example.com
_redirect._._.example.com
```

## Options
### path
**to=** sets the fallback URL, if no specific path subdomain is matched  
**root=** sets the fallback URL, when the root path is requested

### host
**to=** sets the URL to redirect to  
**code=** can change the redirect code used such as 301 or 302
