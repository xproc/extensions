# pxp:message

Output a message.

```xml
<p:declare-step type="pxp:message">
  <p:input port="source" sequence="true"/>
  <p:output port="result" sequence="true"/>
  <p:option name="severity" select="'INFO'"/>  <!-- WARN, INFO, DEBUG -->
  <p:option name="message" required="true"/>
  <p:option name="param{N}"/>
</p:declare-step>
```

This step performs the identity step with the side-effect of
writing a message to an implementation-defined logging
mechanism (for instance simply outputting to the console).

If the `source` port is not explicitly connected, and there
is no default input connection, an empty sequence of documents
are used instead.

The `severity` option must be one of: 'WARN', 'INFO' or
'DEBUG'. The default is 'INFO'. The severity level must be
passed on to the implementation-defined logging mechanism.
It is recommended that the implementation-defined logging
mechanism reflects the severity in its output.

The `message` option contains a text string to be logged.
Occurrences of `${N}` (`$1`, `$2`, etc) will be replaced with
their corresponding `param{N}` options. It is a static error
to reference a `param{N}` that is not defined.

## Example

```xml
<pxp:message message="Processed $1 HTML documents and $2 CSS-files." severity="WARN">
  <p:with-option name="param1" select="count(/*/*)">
    <p:pipe port="name" step="html"/>
  </p:with-option>
  <p:with-option name="param2" select="count(/*/*)">
    <p:pipe port="name" step="css"/>
  </p:with-option>
</pxp:message>
```

...would output something like...

```text
[WARN] Processed 7 HTML documents and 3 CSS-files.
```

## Errors

Error      | Description
---------- | -----------
`err:MU01` | Occurs if the option `param{N}` referenced by `${N}` in the `message` string does not exist.