+++
fragment = "content"
weight = 200

title = "Placeholders"

[sidebar]
  enable = true
+++

# Dynamic Placeholders

Some of the placeholders like `{>Header}` and Regex headers are dynamic and should
get replaced with a key before adding them to the record. We've described all of
these placeholders with more details in the section below.

## Header Placeholders

Using the `{>Header}` placeholder you can use the request's headers inside your
TXT records. To use this placeholder you have to write the header's key after
the `>` symbol. Like `{>Authorization}` or `{>Server}`.

## Regex Placeholders

When a request goes through a `path` record, TXTDirect will add the regex
matches after parsing the path to the placeholders so you can use them inside
your records to have more dynamic redirects. For example after parsing the
`/test/path`, you can use the `{1}` and `{2}` placeholders to access the request
path as placeholders. Each number represents a part of the parsed path and the
order depends on the Regex that parsed the request path.

## Host Label Placeholders

The `{labelN}` placeholder represents the Nth label of the host. `N` is an
integer and starts from 1 like `{label1}` or `{label2}`. For example if the
request's host is `test.example.com`, the placeholders would be like this:

- `{label1}` = test
- `{label2}` = example
- `{label3}` = com

## Query Placeholders

You can use the request's URI queries inside your records using the `{?query}`
placeholder. For example if the request's query is `example.com/?user=admin`,
you can use the `{?user}` placeholder inside the records.
