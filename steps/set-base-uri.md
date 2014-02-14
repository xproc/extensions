# pxp:set-base-uri

A step for changing the base URI of a document.

```xml
<p:declare-step type="pxp:set-base-uri">
  <p:input port="source"/>
  <p:output port="result"/>
  <p:option name="uri" required="true"/>  <!-- string -->
</p:declare-step>
```

The document that appears on the `source` port is copied to the `result` port.
The base URI of the copied document will be the URI specified in the `uri`
option. If the URI specified is relative, it will be made absolute with
respect to the base URI of the option element.

