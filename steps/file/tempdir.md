# pxf:tempdir

Creates a temporary directory.

```xml
<p:declare-step type="pxf:tempdir">
     <p:output port="result" primary="false"/>
     <p:option name="href" required="true"/>           <!-- anyURI -->
     <p:option name="prefix"/>                         <!-- string -->
     <p:option name="suffix"/>                         <!-- string -->
     <p:option name="delete-on-exit"/>                 <!-- boolean -->
     <p:option name="fail-on-error" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

The `pxf:tempdir` step creates a temporary directory. The temporary directory is
guaranteed not to already exist when `pxf:tempdir` is called.

The directory is created in the directory specified by the `href` option. If
`prefix` is specified, the directory's name will begin with that prefix. If
`suffix` is specified, the directory's name will end with that suffix.

The step returns a `c:result` element containing the absolute URI of the
temporary directory.

If the `delete-on-exit` option is `true`, then the temporary directory will
automatically be deleted when the processor terminates.

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if `href` does not specify a directory or
           | if the directory does not exist.
`err:FU04` | Occurs if it is not possible to create a directory in the `href` directory.
