# pxf:tempfile

Creates a temporary file.

```xml
<p:declare-step type="pxf:tempfile">
     <p:output port="result" primary="false"/>
     <p:option name="href" required="true"/>           <!-- anyURI -->
     <p:option name="prefix"/>                         <!-- string -->
     <p:option name="suffix"/>                         <!-- string -->
     <p:option name="delete-on-exit"/>                 <!-- boolean -->
     <p:option name="fail-on-error" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

The `pxf:tempfile` step creates a temporary file. The temporary file is
guaranteed not to already exist when `pxf:tempfile` is called.

The file is created in the directory specified by the `href` option. If
`prefix` is specified, the file's name will begin with that prefix. If
`suffix` is specified, the file's name will end with that suffix.

The step returns a `c:result` element containing the absolute URI of the
temporary file.

If the `delete-on-exit` option is `true`, then the temporary file will
automatically be deleted when the processor terminates.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if `href` does not specify a directory or
           | if the directory does not exist.
`err:FU04` | Occurs if it is not possible to create a file in the `href` directory.
