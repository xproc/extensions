# pxf:delete

Deletes a file.

```xml
<p:declare-step type="pxf:delete">
  <p:output port="result" primary="false"/>
  <p:option name="href" required="true"/>          <!-- anyURI -->
  <p:option name="recursive" select="'false'"/>    <!-- boolean -->
  <p:option name="fail-on-error" select="'true'"/> <!-- boolean -->
</p:declare-step>
```

The `pxf:delete` step attempts to delete the file or directory named in
`href`.

If the file or directory is successfully deleted, the step returns a
`c:result` element containing the absolute URI of the deleted file.

If `href` specifies a directory, it can only be deleted if the `recursive`
option is `true` or if the directory is empty.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if the file named in `href` does not exist
           | or cannot be deleted.
`err:FU02` | Occurs if the step attempts to delete a directory
           | that is not empty and the `recursive` option is not `true`.
