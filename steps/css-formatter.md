# p:css-formatter

The p:xsl-formatter step receives an XML or HTML document and renders the content according to the CSS stylesheet(s) on the `stylesheet` port. The result of rendering is stored to the URI provided via the `href` option. A reference to that result is produced on the output port.

````
<p:declare-step type="p:css-formatter">
  <p:input port="source"
           content-types="application/xml text/xml */*+xml text/html"/>
  <p:input port="stylesheet" content-types="text/css"/>
  <p:output port="result"/>
  <p:option name="parameters" as="map(xs:QName,item())"/>
  <p:option name="href" required="true" as="xs:anyURI"/>
  <p:option name="content-type" as="xs:string"/>
</p:declare-step>
````

The value of the `href` option must be an `anyURI`. If it is relative, it is made absolute against the base URI of the element on which it is specified (p:with-option or p:css-formatter in the case of a syntactic shortcut value).

The content-type of the output is controlled by the content-type option. This option specifies a media type as defined by [IANA Media Types]. The option may include media type parameters as well (e.g. "application/someformat; charset=UTF-8"). The use of media type parameters on the content-type option is implementation-defined.

If the content-type option is not specified, the output type is implementation-defined. The default should be PDF.

A formatter may take any number of optional rendering parameters via the step's parameters; such parameters are defined by the CSS implementation used and are implementation-defined.

The output of this step is a document containing a single c:result element whose content is the absolute URI of the document stored by the step.
