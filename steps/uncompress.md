# pxp:uncompress

A step for expanding compressed data.

```xml
<p:declare-step type="pxp:uncompress">
  <p:input port="source"/>
  <p:output port="result"/>
  <p:option name="compression-method"/>  <!-- string -->
</p:declare-step>
```

If the document that appears on the `source` port is `base64` encoded, this
step will decode and attempt to uncompress the data. As a convenience, if the
data is not encoded, the XML document is simply passed through, like the
`p:identity` step.

The `compression-method` option can be used to identify the compression method
used. Suggested values are “`bzip2`”, “`compress`”, “`gzip`”, etc. If
unspecified, implementations are free to attempt to deduce the method from the
data.

It is a _dynamic error_ if:

* the compression method is unrecognized or
* the resulting, decoded and expanded data is not a well-formed XML document.
