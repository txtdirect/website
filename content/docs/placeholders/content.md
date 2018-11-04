+++
fragment = "content"
weight = 200

title = "Placeholders"

[sidebar]
  enable = true
+++

TXTDirect supports various placeholders. These can be used to create more dynamic redirects.

|Placeholder	       |Value |
|--------------------|------|
|**{~cookie}**       |The value of a cookie, where "cookie" is the cookie name |
|**{dir}**           |The directory of the requested file (from request URI) |
|**{file}**          |The name of the requested file (from request URI) |
|**{fragment}**      |The last part of the URL starting with "#" |
|**{>Header}**       |Any request header, where "Header" is the header field name |
|**{host}**          |The host value on the request |
|**{hostonly}**      |Same as {host} but without port information |
|**{labelN}**        |The Nth label of the host (where N is an integer, at least 1) such as {label1}.{label2}.{label3}. |
|**{method}**        |The request method (GET, POST, etc.) |
|**{path}**          |The path portion of the original request URI (does not include query string or fragment) |
|**{path_escaped}**  |Query-escaped variant of {path} |
|**{port}**          |The client's port |
|**{query}**         |The query string portion of the URL, without leading "?" |
|**{query_escaped}** |The query-escaped variant of {query} |
|**{?key}**          |The value of the "key" argument from the query string |
|**{uri}**           |The request URI (includes path, query string, and fragment) |
|**{uri_escaped}**   |The query-escaped variant of {uri} |
|**{user}**          |The username authorized by basicauth (HTTP Basic Authentication) |
