# p:error

This is a proposed change to the `p:error` step.

```xml
<p:declare-step type="p:error">
  <p:output port="result" sequence="true"/>
  <p:option name="code" required="true"/> <!-- QName -->
  <p:option name="code-prefix"/> <!-- NCName -->
  <p:option name="code-namespace"/> <!-- anyURI -->
  <p:option name="message" required="true"/>
  <p:option name="param{N}"/>
</p:declare-step>
```

Changes from v1:
* The input port has been dropped and replaced with a "message" option.
* `param{N}` options are accepted for use as replacements for `${N}` in the message string.

The `message` option contains a text string to be used as the error message. Occurrences of `${N}` (`$1`, `$2`, etc) will be replaced with their corresponding `param{N}` option. It is a static error to reference a `param{N}` that is not defined.

## Example

```xml
<p:error message="There must be an equal number of HTML and SMIL documents. Found $1 HTML documents and $2 SMIL documents.">
  <p:with-option name="param1" select="count(/*/*)">
    <p:pipe port="name" step="html"/>
  </p:with-option>
  <p:with-option name="param2" select="count(/*/*)">
    <p:pipe port="name" step="smil"/>
  </p:with-option>
</p:error>
```

...might output something like...

```text
[ERROR] There must be an equal number of HTML and SMIL documents. Found 7 HTML documents and 3 SMIL documents.
```

## Errors

Error      | Description
---------- | -----------
`err:MU01` | Occurs if the option `param{N}` referenced by `${N}` in the `message` string does not exist.