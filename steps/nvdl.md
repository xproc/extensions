# pxp:nvdl

A step for performing [NVDL](http://www.nvdl.org/) (Namespace-based Validation
Dispatching Language) validation over mixed-namespace documents.

```xml
<p:declare-step type="pxp:nvdl">
  <p:input port="source" primary="true"/>
  <p:input port="nvdl"/>
  <p:input port="schemas" sequence="true"/>
  <p:output port="result"/>
  <p:option name="assert-valid" select="'true'"/>  <!-- boolean -->
</p:declare-step>
```

The `source` document is validated using the namespace dispatching rules
contained in the `nvdl` document.

The dispatching rules may contain URI references that point to the actual
schemas to be used. As long as these schemas are accessible, it is not
necessary to pass anything on the `schemas` port. However, if one or more
schemas are provided on the `schemas` port, then these schemas should be used
in validation.

This requirement is expressed only as a “should” and not a “must” because
XProc version 1.0 does not mandate that implementations support caching of
documents so that requests for a URI by one step can automatically access the
result of some other step if that result had a base URI identical to the
requested document.

However, it's not clear that the `schemas` port has any value if the
implementation does not support this behavior.

The value of the `assert-valid` option must be a boolean. It is a _dynamic
error_ if the `assert-valid` option is `true` and the input document is not
valid.

The output from this step is a copy of the input, possibly augmented by
application by schema processing. The output of this step may include PSVI
annotations.

