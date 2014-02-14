# pxf:head

Returns the first few lines of text file.

```xml
<p:declare-step type="pxf:head">
  <p:output port="result"/>
  <p:option name="href" required="true"/>           <!-- anyURI -->
  <p:option name="count" required="true"/>          <!-- int -->
  <p:option name="fail-on-error" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

Returns the first `count` lines of the file named in `href`. If `count` is
negative, the step returns all _except_ those first lines.

The step returns a `c:result` element containing one `c:line` for each line.
Lines are identified as described in XML, [2.11 End-of-Line
Handling](http://www.w3.org/TR/xml/#sec-line-ends).

If an error occurs, the step fails if `fail-on-error` is `true`; otherwise,
the step returns a `c:error` element which may contain additional,
implementation-defined information about the nature of the error.

## Errors

Error      | Description
---------- | -----------
`err:FU01` | Occurs if the file named in `href` does not exist or cannot be read.
`err:FU03` | Occurs if the file named in `href` does not appear to be a text
           | file. The exact conditions that constitute “does not appear to
           | be” are implementation-defined.

