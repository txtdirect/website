+++
fragment = "item"
date = "2018-09-08"
weight = 320
background = "light"
align = "left"

subtitle = "Path redirect with custom order"

pre = "*s.txtdirect.org/v2/docs/*"
post = "*docs.txtdirect.org/v2*"

[asset]
  icon = "fas fa-arrow-down"
+++

* Point your chosen subdomain CNAME to **txtd.io.**
* Create a TXT record with the subdomain **_redirect**
* Use the open TXTDirect spec to configure your redirect

```text
s.txtdirect.org                 86000 IN CNAME   txtd.io.
_redirect.s.txtdirect.org       86400 IN TXT     "v=txtv0;type=path;from=/$2/$1/;to=https://about.txtdirect.org;root=https://about.txtdirect.org"

_redirect.v2.docs.s.txtdirect.org   86400 IN TXT     "v=txtv0;type=host;code=302;to=https://docs.txtdirect.org/v2"

_redirect._._.s.txtdirect.org   86400 IN TXT     "v=txtv0;type=host;code=302;to=https://about.txtdirect.org/hosted"
```

Instead of the default lookup order TXTDirect allows a custom order to be set using the **from**. Using **/$2/$1** would reverse the default order.

### Options
#### path
**to=** sets the fallback URL, if no specific path subdomain is matched  
**root=** sets the fallback URL, when the root path is requested
**from=** enables reordering such as **/$2/$1/**

#### host
**to=** sets the URL to redirect to  
**code=** can change the redirect code used such as 301 or 302
