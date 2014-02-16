# pxp:assert

Conditionally output a message or throw an error.

```xml
<p:declare-step type="pxp:assert">
  <p:input port="source" sequence="true"/>
  <p:output port="result" sequence="true"/>
  <p:option name="test" required="true"/>
  <p:option name="equals"/>
  <p:option name="message" required="true"/>
  <p:option name="code"/> <!-- QName -->
  <p:option name="code-prefix"/> <!-- NCName -->
  <p:option name="code-namespace"/> <!-- anyURI -->
  <p:option name="param{N}"/>
</p:declare-step>
```

The `message` option contains a text string to be reported in
case the assertion fails. Occurrences of `${N}` (`$1`, `$2`,
etc) will be replaced with their corresponding `param{N}`
options. It is a static error to reference a `param{N}` that
is not defined.

The value of `test` and `equals` are passed to the
implementation-defined logging system, which may use the
values to produce more information about the failed assertion
to the user.

If the `source` port is not explicitly connected, and there is
no default input connection, an empty sequence of documents
are used instead.

 1. If `test` equals `equals` (or if `equals` is not defined and
    `test`s effective boolean value is `true()`), this step
    performs an identity step. No messages are output and no
    errors are thrown.
    
 2. If `test` does not equal `equals` (or if `equals` is not
    defined and `test`s effective boolean value is `false()`)
    and the `code` option is provided, then this step behaves
    exactly like `p:error`.
    
 3. If `test` does not equal `equals` (or if `equals` is not
    defined and `test`s effective boolean value is `false()`)
    and the `code` option is *not* provided, this step performs
    the identity step with the side-effect of writing a message
    to an implementation-defined logging mechanism (for instance
    simply outputting to the console). The severity 'WARN' will
    be passed to the logging mechanism. It is recommended that
    the implementation-defined logging mechanism reflects the
    severity in its output.

## Example

```xml
<pxp:assert message="The document should have a head element" test="/*/head"/>
<pxp:assert message="There must be exactly one body element (source: $1)." test="count(/*/body)" equals="1" code="my:ERROR01">
  <p:with-option name="param1" select="base-uri(/*)">
    <p:pipe port="result" step="input-document"/>
  </p:with-option>
</pxp:assert>
```

...might output something like...

```text
[WARN] The document should have a head element.
[ERROR] There must be exactly one body element (source: file:/tmp/input.xml).
    was: 0
    expected: 1
```

## Errors

Error      | Description
---------- | -----------
`err:MU01` | Occurs if the option `param{N}` referenced by `${N}` in the `message` string does not exist.