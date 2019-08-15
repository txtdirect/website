+++
fragment = "content"
weight = 100

title = "Configuration"

[sidebar]
  enable = true
  sticky = true
+++

# Redirect Types

---

### Supported redirect types:

| Type Name | Type Information                                            |
| --------- | ----------------------------------------------------------- |
| www       | Redirect all requests to "www"-subdomain                    |
| host      | Redirect to host provided in TXT record                     |
| path      | Enable path based redirects                                 |
| gometa    | Enable Go packages meta/vanity redirects                    |
| gomods    | Enable serving and caching Go modules                       |
| dockerv2  | Redirect to docker registry or image provided in TXT record |
| proxy     | Proxy the request to endpoint provided in TXT record        |

---

### Enable types

```
txtdirect {
  enable www
}
```

### Enable multiple types

```
txtdirect {
  enable host path gomods dockerv2
}
```

### Disable types

```
txtdirect {
  disable www
}
```

# Fallback

## Flow

Step-by-Step fallback flow:

- Specific record's `to=` field
- Specific record's `website=` field
- Specific record's `root=` field
- Second to last record's `website=` field
- Second to last record's `root=` field
- Second to last record's `to=` field
- Request's host "www"-subdomain
- Global config's `redirect` field
- 404 Status code

_hint: **Specific record** is the last TXT record found_  
_hint 2: **Second to last record** is the last path record leading to the **Specific record**_

## Global fallback config

### Enable "www"-subdomain fallback

```
txtdirect {
  enable www
}
```

### Default `redirect` fallback

```
txtdirect {
  redirect https://example.com
}
```
