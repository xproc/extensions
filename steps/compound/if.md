# pxc:if

A `if` specifies one subpipeline guarded by a test expression.

```xml
<pxc:if
  test = XPathExpression>
    (p:xpath-context?,
     (p:output |
      p:log)*,
     subpipeline)
</pxc:if>
```

`pxc:if` has a test attribute which must contain an XPath expression.
That XPath expression's effective boolean value is the guard for the
subpipeline contained within that pxc:if.

The `pxc:if` can specify a context node against which its test
expression is to be evaluated. That context node is specified as a
connection for the p:xpath-context. If no explicit connection is
provided, the default readable port is used.

The outputs of the `pxc:if` are taken from the outputs of the
subpipeline. If the test expression fails, then the primary output
port (if present) are connected to the default readable port, and all
other ports will output empty sequences (as if connected to
`p:empty`).

In other words, this pipleine:

```xml
<p:declare-step xmlns:p="http://www.w3.org/ns/xproc"
                xmlns:exf="http://exproc.org/standard/functions"
                version="1.0" name="main">
<p:input port="source"/>
<p:input port="parameters" kind="parameter"/>
<p:output port="result"/>

<p:if test="false()">
  <p:output port="primary" primary="true"/>
  <p:output port="secondary">
    <p:pipe step="xslt" port="result"/>
  </p:output>

  <p:xslt name="xslt">
    <p:input port="stylesheet">
      <p:document href="docbook.xsl"/>
    </p:input>
  </p:xslt>
</p:if>

</p:declare-step>
```

is equivalent to this one:

```xml
<p:declare-step xmlns:p="http://www.w3.org/ns/xproc"
                xmlns:exf="http://exproc.org/standard/functions"
                version="2.0" name="main">
<p:input port="source"/>
<p:input port="parameters" kind="parameter"/>
<p:output port="result"/>

<p:choose>
  <p:when test="false()">
    <p:output port="primary" primary="true"/>
    <p:output port="secondary">
      <p:pipe step="xslt" port="result"/>
    </p:output>

    <p:xslt name="xslt">
      <p:input port="stylesheet">
        <p:document href="docbook.xsl"/>
      </p:input>
    </p:xslt>
  </p:when>
  <p:otherwise>
    <p:output port="primary" primary="true"/>
    <p:output port="secondary">
      <p:empty/>
    </p:output>
    <p:identity/>
  </p:otherwise>
</p:choose>

</p:declare-step>
```
