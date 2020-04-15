+++
fragment = "content"
weight = 200

title = "Basics"

[sidebar]
  enable = true
+++

To use TXTDirect's hosted service you first have to add a `CNAME` or `A` record
to your DNS zone file that points to the hosted service's domain which is
`txtd.io`.

The reason that you need these records is that when `txtd.io` receives
a request, it will look for a `TXT` record on the `_redirect.example.com` zone,
which `example.com` stands for the incoming request's host. So when you point
the `CNAME` or `A` records to `txtd.io`, TXTDirect will look for the `TXT`
records on your zone file using the request's host.
So you can host your zone file anywhere using any tool you like, and let
`txtd.io` take care of your redirects.

Adding a new record can be different based on your DNS service provider but in
general the added record should look like this:

```
a.example.com                    86000 IN CNAME   txtd.io.
```

Note: Keep in mind that `CNAME` records only work on subdomains, so if you want
to redirect the incoming requests to your root record, you have to add `A` and
`AAAA` records to your zone file.

The records for a root redirect should look like this:

```
example.com             86000 IN A       45.85.238.5
example.com             86000 IN AAAA    2a0e:c885:5::1
```

Now that the `CNAME` or `A` records are setup, you can start adding the `TXT`
records. For example, to redirect the requests for `git.example.com` to
`github.com/example`, you can add the following records to your zone file.

```
git.example.com             86000 IN CNAME   txtd.io.
_redirect.git.example.com   86000 IN TXT     "v=txtv0;type=host;to=https://github.com/example"
```

So the example above points `git.example.com` to TXTDirect's servers and when
TXTDirect receives a request for `git.example.com`, it will look for a `TXT`
record with the `_redirect.git.example.com` address. Then it will redirect the
requests based on the `TXT` record's type and endpoint, which in case of this
example, it redirects the requests without any additional check and logic to
the endpoint specified in the `to=` field.

You can use all of TXTDirect's types and features on the hosted service too and
the only thing that is different compared to running your instance is that
you have to point each domain to `txtd.io` before writing its TXT records like
the examples above.

Take a look at the [Basic Configuration](/docs/config/basics/) page to learn
more about TXTDirect's types and how they work. The [Specification](/docs/specification) page details the available types. Additional
[Record Examples](/docs/examples) give some ideas for each type and
more complex examples like combining the types.
