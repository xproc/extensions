# pxf:copy

Copies a file.

```xml
<p:declare-step type="pxf:copy">
   <p:output port="result" primary="false"/>
   <p:option name="href" required="true"/>          <!-- anyURI -->
   <p:option name="target" required="true"/>        <!-- boolean -->
   <p:option name="fail-on-error" select="'true'"/> <!-- boolean-->
</p:declare-step>
```

The `pxf:copy` copies the file named in `href` to the new name specified in
`target`. If the `target` is a directory, the step attempts to move the file
into that directory, preserving its base name.

If the copy is successful, the step returns a `c:result` element containing
the absolute URI of the target.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if the file named in `href` does not exist or cannot
           | be copied to the specified target.

