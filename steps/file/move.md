# pxf:move

Moves (renames) a file or directory.

```xml
<p:declare-step type="pxf:move">
  <p:output port="result" primary="false"/>
  <p:option name="href" required="true"/>            <!-- anyURI -->
  <p:option name="target" required="true"/>          <!-- boolean -->
  <p:option name="fail-on-error" select="'true'"/>   <!-- boolean -->
</p:declare-step>
```

The `pxf:move` step attempts to move (rename) the file specified in the `href`
option to the new name specified in the `target` option.

If the `target` is a directory, the step attempts to move the file into that
directory, preserving its base name.

If the move is successful, the step returns a `c:result` element containing
the absolute URI of the new name of the file. The original file is effectively
removed.

If the `fail-on-error` option is `true`, then the step will fail if a file
with the name specified in the `target` option already exists, or if the file
specified in `href` does not exist or cannot be moved.

If the `fail-on-error` option is `false`, the step returns a `c:error` element
which may contain additional, implementation-defined information about the
nature of the error.

If the `href` option specifies a directory, device, other special kind of
object, the results are implementation-defined.
