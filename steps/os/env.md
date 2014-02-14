# pos:env

Returns information about the environment

```xml
<p:declare-step type="pos:env">
  <p:output port="result"/>
</p:declare-step>
```

The `pos:env` step returns information about the operating system environment.
It returns a `c:result` containing zero or more `c:env` elements. Each `c:env`
has `name` and `value` attributes containing the name and value of an
environment variable.

On systems which nave no concept of an environment, this step returns an empty
`c:result`.
