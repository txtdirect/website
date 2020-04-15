+++
fragment = "content"
weight = 200

title = "Path with other types"

[sidebar]
  enable = true
+++

The `path` type can also be used with other types like `gometa` or `host`.
This feature enables you to redirect requests based on their path to different
endpoints. For example, we use this feature to create vanity URLs for
our packages. Take a look at this example:

```
pkg.example.com                     3600 IN A      127.0.0.1
_redirect.pkg.example.com           3600 IN TXT    "v=txtv0;type=path"
_redirect.foo.pkg.example.com       3600 IN TXT    "v=txtv0;type=gometa;to=https://github.com/foo/foo"
_redirect.bar.pkg.example.com       3600 IN TXT    "v=txtv0;type=gometa;to=https://github.com/foo/bar"
_redirect.baz.pkg.example.com       3600 IN TXT    "v=txtv0;type=host;to=https://github.com/foo/baz/blob/master/README.md#deprecated"
```

Using these records we can setup the following redirects:  
**pkg.example.com/foo -> https://github.com/foo/foo**  
**pkg.example.com/bar -> https://github.com/foo/bar**  
**pkg.example.com/baz -> https://gcr.io/foo/baz**

But these redirects are not just simple redirects because we've used `gometa` and
`host` types in this example. To learn more about what each type can do
check out the full [specification](/docs/specification).

We can use the records from the example above in `go get` command and the
Docker CLI. For example, we can use them like this:

```
$ go get pkg.example.com/foo
$ go get pkg.example.com/bar
$ docker pull pkg.example.com/baz
```
