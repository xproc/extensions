# pos:cwd

Returns the current working directory of the processor.

```xml
<p:declare-step type="pos:cwd">
  <p:output port="result" sequence="true"/>
</p:declare-step>
```

The `pos:cwd` step returns a single `c:result` containing the current working
directory. On systems which have no concept of a working directory, this step
returns the empty sequence.

(This step is exactly duplicates the `cwd` attribute on the `c:result` from
`pos:info`; it's just for convenience.)
