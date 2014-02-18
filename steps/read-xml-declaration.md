# pxp:read-xml-declaration

Reads the XML declaration from an XML file.

```xml
<pxp:read-xml-declaration>
  <p:output port="result"/>
  <p:option name="href" required="true"/> <!-- anyURI -->
</pxp:read-xml-declaration>
```

From the [XPath 1.0 specification](http://www.w3.org/TR/xpath/#section-Processing-Instruction-Nodes)

> **NOTE**: The XML declaration is not a processing instruction. Therefore, there is no processing instruction node corresponding to the XML declaration.

After loading a document, there is no way to determine whether or not it contained an XML declaration (or what values that XML declaration contained). Also, some times it is useful to read the XML declaration without loading the entire file (for instance for validation purposes). The signature of this step is similar to that of `p:load`, but instead of loading the file, it reads the XML declaration of that file.

The `result` output port will contain a `c:result` document. If there is no XML declaration, then the result document will not contain any attributes. If an XML declaration is found, the attributes in the XML declaration will be provided as attributes on the resulting `c:result` document:

```xml
<c:result
  version? = string
  encoding? = string
  standalone? = string />
```

## Errors

Error        | Description
------------ | -----------
`err:XC0027` | Occurs if the file named in `href` does not exist or is not valid.
