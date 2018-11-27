+++
fragment = "content"
weight = 100

title = "Configuration"

[sidebar]
  enable = true
+++

**Redirect all requests to "www"-subdomain:**  
*example.com -> www.example.com*
```
txtdirect {
  enable www
}
```

**Redirect to host provided in TXT record:**  
*Fallback: Return 404 on empty record*
```
txtdirect {
  enable host
}
```

**Redirect to host provided in TXT record:**  
*Fallback: Redirect to "www"-subdomain on empty record*
```
txtdirect {
  enable host www
}
```

**Redirect to host provided in TXT record:**  
*Fallback: Redirect to example.com on empty record*
```
txtdirect {
  redirect https://example.com
}
```

**Enable path based redirects:**  
```
txtdirect {
    enable host path
}
```

**Enable go meta/vanity redirects:**  
*pkg.example.com -> github.com/some/pkg.git*
```
txtdirect {
  enable gometa
}
```

**Enable everything except "www"-subdomain redirection:**  
```
txtdirect {
    disable www
}
```