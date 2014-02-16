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

`pxc:if` has a test attribute which must contain an XPath expression. That XPath expression's effective boolean value is the guard for the subpipeline contained within that pxc:if.

The `pxc:if` can specify a context node against which its test expression is to be evaluated. That context node is specified as a connection for the p:xpath-context. If no explicit connection is provided, the default readable port is used.

The outputs of the `pxc:if` are taken from the outputs of the subpipeline. If the test expression fails, then the primary output port (if present) are connected to the default readable port, and all other ports will output empty sequences (as if connected to `p:empty`).
