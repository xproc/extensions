# pxf:touch

Update the modification time of a file.

```xml
<p:declare-step type="pxf:touch">
  <p:output port="result" primary="false"/>
  <p:option name="href" required="true"/>           <!-- anyURI -->
  <p:option name="timestamp"/>                      <!-- xs:dateTime -->
  <p:option name="fail-on-error" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

The `pxf:touch` step “touches” the file named in `href`. The file will be
created if it does not exist.

If `timestamp` is specified, the modification time of the file will be updated
to the specified time. If unspecified, the current date and time will be used.

The step returns a `c:result` element containing the absolute URI of the
touched file.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if the file named in `href` does not exist or
           | if its timestamp cannot be changed.

