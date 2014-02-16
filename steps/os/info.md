# pos:info

Returns information about the operating system.

```xml
<p:declare-step type="pos:info">  
  <p:output port="result"/>  
</p:declare-step>
```

The `pos:info` step returns information about the operating system on which
the processor is running. It returns a `c:result` element with attributes
describing properties of the system. It _should_ include the following
properties:

Attribute name     | Attribute value
------------------ | ----------------------
`file-separator`   | The file separator; usually “/” on Unix, “\” on Windows.
`path-separator`   | The path separator; usually “:” on Unix, “;” on Windows.
`os-architecture`  | The operating system architecture, for example “i386”.
`os-name`          | The name of the operating system, for example “Mac OS X”.
`os-version`       | The version of the operating system, for example “10.5.6”.
`cwd`              | The current working directory.
`user-name`        | The login name of the effective user, for example “ndw”.
`user-home`        | The home diretory of the effective user, for example “/home/ndw”.
`temp-dir`         | The operating system temporary directory, for example “file:/tmp/”

The exact set of properties returned is implementation-dependent.

