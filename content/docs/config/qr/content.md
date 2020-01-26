+++
fragment = "content"
weight = 200

title = "QR"

[sidebar]
  enable = true
  sticky = true
+++

By enabling QR, if the incoming request has a "?qr" query, TXTDirect will serve the request's URI QR code.

# Config

---

By providing additional configs like size, background color, and foreground color you can configure how the generated QR codes look.

### Enable QR

```
txtdirect {
  qr
}
```

### Advanced config

```
txtdirect {
  qr {
    size 512
    background #ffffff
    foreground #000000
  }
}
```
