# pxp:zip

A step for creating ZIP archives.

```xml
<p:declare-step type="pxp:zip">
  <p:input port="source" sequence="true" primary="true"/>
  <p:input port="manifest"/>
  <p:output port="result"/>
  <p:option name="href" required="true"/>       <!-- anyURI -->
  <p:option name="compression-method"/>         <!-- "stored" | "deflated" -->
  <p:option name="compression-level"/>          <!-- "smallest" | "fastest" | "default" | "huffman" | "none" -->
  <p:option name="command" select="'update'"/>  <!-- "update" | "freshen" | "create" | "delete" -->
</p:declare-step>
```

The ZIP archive is identified by the `href`. The `manifest` (described below)
provides the list of files to be processed in the archive. The `command`
indicates the nature of the processing: “`update`”, “`freshen`”, “`create`”,
or “`delete`”.

If files are added to the archive, `compression-method` indicates how they
should be added: “`stored`” or “`deflated`”. For deflated files, the
`compression-level` identifies the kind of compression: “`smallest`”,
“`fastest`”, “`default`”, “`huffman`”, or “`none`”.

The entries identified by the `manifest` are processed. The manifest must
conform to the
[zip-manifest.rnc](schemas/zip-manifest.rnc) schema.

For example:

```xml
<zip-manifest xmlns="http://www.w3.org/ns/xproc-step">
  <entry name="file1.xml" href="http://example.org/file1.xml" comment="An example file"/>
  <entry name="path/to/file2.xml" href="http://example.org/file2.xml" method="stored"/>
</zip-manifest>
```

If the `command` is “`delete`”, then `file1.xml` and `path/to/file2.xml` will
be deleted from the archive. Otherwise, the file that appears on the `source`
port that has the base URI `http://example.org/file1.xml` will be stored in
the archive as `file1.xml` (using the default method and level), the file that
appears on the `source` port that has the base URI
`http://example.org/file2.xml` will be stored in the archive as
`path/to/file2.xml` without being compressed.

A `c:zipfile` description of the archive content is produced on the `result`
port.

