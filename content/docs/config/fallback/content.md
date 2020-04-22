+++
fragment = "content"
weight = 101

title = "Fallback"

[sidebar]
  enable = true
  sticky = true
+++

## Flow

---

Step-by-Step fallback flow:

- Current TXT record's `to=` field
- Current TXT record's `website=` field
- Current TXT record's `root=` field
- Parent (type=path) TXT record's `website=` field
- Parent (type=path) TXT record's `root=` field
- Parent (type=path) TXT record's `to=` field
- Request's host "www"-subdomain (if enabled)
- Global config's `redirect` field (if configured)
- 404 Status code

## Global fallback config

---

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
