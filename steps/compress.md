# pxp:compress

A step for storing compressed data.

```xml
<p:declare-step type="pxp:compress">
  <p:input port="source"/>
  <p:output port="result"/>
  <p:option name="href"/>                                    <!-- anyURI -->
  <p:option name="compression-method"/>                      <!-- string -->
  <p:option name="byte-order-mark"/>                         <!-- boolean -->
  <p:option name="cdata-section-elements" select="''"/>      <!-- ListOfQNames -->
  <p:option name="doctype-public"/>                          <!-- string -->
  <p:option name="doctype-system"/>                          <!-- anyURI -->
  <p:option name="encoding"/>                                <!-- string -->
  <p:option name="escape-uri-attributes" select="'false'"/>  <!-- boolean -->
  <p:option name="include-content-type" select="'true'"/>    <!-- boolean -->
  <p:option name="indent" select="'false'"/>                 <!-- boolean -->
  <p:option name="media-type"/>                              <!-- string -->
  <p:option name="method" select="'xml'"/>                   <!-- QName -->
  <p:option name="normalization-form" select="'none'"/>      <!-- NormalizationForm -->
  <p:option name="omit-xml-declaration" select="'true'"/>    <!-- boolean -->
  <p:option name="standalone" select="'omit'"/>              <!-- "true" | "false" | "omit" -->
  <p:option name="undeclare-prefixes"/>                      <!-- boolean -->
  <p:option name="version" select="'1.0'"/>                  <!-- string -->
</p:declare-step>
```

The `pxp:compress` step serializes the document that appears on its `source`
port and compresses it. If the input document is `base64` encoded, it is
decoded and the corresponding bytes are compressed.

The `compression-method` option can be used to identify the compression method
used. Suggested values are “`bzip2`”, “`compress`”, “`gzip`”, etc. If
unspecified, the default method is _implementation defined_.

> Note
> Would it be better to specify a default? Perhaps `gzip`?

It is a _dynamic error_ if the method is unrecognized.

If the `href` attribute is present, the step attempts to store the compressed
data to the IRI specified. In this case, it produces a `c:result` element on
its `result` port that contains the IRI where the data was stored.

If the `href` attribute is not present, the step returns the compressed data
in a `base64` encoded `c:data` element with an appropriate `content-type`.
