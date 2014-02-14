# pxf:mkdir

Creates a directory.

```xml
<p:declare-step type="pxf:mkdir">
  <p:output port="result" primary="false"/>
  <p:option name="href" required="true"/>           <!-- anyURI -->
  <p:option name="fail-on-error" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

The `pxf:mkdir` step creates a directory with the name in `href`. If the name
includes more than one directory component, all of the intermediate components
are created. The path separator is implementation-defined.

The step returns a `c:result` element containing the absolute URI of the
directory created.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if the directory named in `href` cannot be created.
