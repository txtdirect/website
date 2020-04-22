+++
fragment = "content"
title = "Configuration"
weight = 100

[sidebar]
  enable = true
+++

TXTDirect uses [Caddy's](https://caddyserver.com) config controller so all the config files should follow the [Caddyfile syntax](https://caddyserver.com/v1/tutorial/caddyfile) rules.

TXTDirect's reads its config from the `txtdirect` scope in the Caddyfile. For example, using the following config you can tell TXTDirect to enable the `host` redirect type on the `example.com` host and write the logs to `stdout`:

```
example.com:8080 {
  errors stdout
  txtdirect {
    enable host
    logfile stdout
  }
}
```

Some of TXTDirect's features like Prometheus metrics or QR need to be configured separately.
These features need to be configured inside a separate scope like the example below:

```
example.com:8080 {
  txtdirect {
    enable host
    prometheus {
      address 192.168.0.1
    }
  }
}
```

These features are documented in more detail in separate sections within our
[documentation](/docs/config) under the configuration category.

## CLI Flags

Use the `-conf` flag to pass a config file to TXTDirect.

```
$ txtdirect -conf PATH_TO_CONFIG
```

---

If anything is not documented or needs more details, feel free to open an issue or contribute by opening a pull request.

_See how you can contribute with our [contribution guide](https://github.com/txtdirect/website/CONTRIBUTING.md)._
