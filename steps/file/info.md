# pxf:info

Returns information about a file or directory.

```xml
<p:declare-step type="pxf:info">
     <p:output port="result" sequence="true"/>
     <p:option name="href" required="true"/>           <!-- anyURI -->
     <p:option name="fail-on-error" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

The `info` step returns information about the file or directory named in
`href`.

The step returns a `c:directory` for directories, a `c:file` for ordinary
files, or a `c:other` for other kinds of filesystem objects. Implementations
may also return more specific types, for example `c:device`, so anything other
than `c:directory` or `c:file` must be interpreted as “other”. If the document
doesn't exist, an empty sequence is returned.

The document element of the result, if there is one, will have the following
attributes:

Attribute  | Type       | Description
---------- | ---------- | ------------
readable   | xs:boolean | “`true`” if the object is readable.
writable   | xs:boolean | “`true`” if the object file is writable.
hidden     | xs:boolean | “`true`” if the object is hidden.
last-modified | xs:dateTime | The last modification time of the object expressed in UTC.
size       | xs:integer | The size of the object in bytes.

If the value of a particular attribute is unknown or inapplicable for the
particular kind of object, or in the case of boolean attributes, if it's
false, then the attribute is not present. Additional implementation-defined
attributes may be present, but they must be in a namespace.

If the `href`
attribute specified is not a `file:` URI, then the result is implementation-
defined.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if the file named in `href` cannot be read.

