# pxp:unzip

A step for extracting information out of ZIP archives.

```xml
<p:declare-step type="pxp:unzip">
  <p:output port="result"/>
  <p:option name="href" required="true"/>  <!-- anyURI -->
  <p:option name="file"/>                  <!-- string -->
  <p:option name="content-type"/>          <!-- string -->
</p:declare-step>
```

The value of the `href` option must be an IRI. It is a _dynamic error_ if the
document so identified does not exist or cannot be read.

The value of the `file` option, if specified, must be the fully qualified
path-name of a document in the archive. It is _dynamic error_ if the value
specified does not identify a file in the archive.

The output from the `pxp:unzip` step must conform to the
[zip-toc.rnc](schemas/zip-toc.rnc) schema.

If the `file` option is specified, the selected file in the archive is
extracted and returned:

* If the `content-type` is not specified, or if an XML content type is
  specified, the file is parsed as XML and returned. It is a _dynamic
  error_ if the file is not well-formed XML.
* If the `content-type` specified is not an XML content type, the file
  is base64 encoded and returned in a single `c:data` element.

If the `file` option _is not_ specified, a table of contents for the archive
is returned.

For example, the contents of the XML Calabash 0.8.5 distribution archive might
be reported like this:

```xml
<c:zipfile xmlns:c="http://www.w3.org/ns/xproc-step"
           href="http://xmlcalabash.com/download/calabash-0.8.5.zip">
   <c:directory name="calabash-0.8.5/" date="2008-11-04T19:29:20.000-05:00"/>
   <c:directory name="calabash-0.8.5/docs/" date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="11942"
           size="36677"
           name="calabash-0.8.5/docs/CDDL+GPL.txt"
           date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="928"
           size="2110"
           name="calabash-0.8.5/docs/ChangeLog"
           date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="6817"
           size="17987"
           name="calabash-0.8.5/docs/GPL.txt"
           date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="494"
           size="830"
           name="calabash-0.8.5/docs/NOTICES"
           date="2008-11-04T19:29:20.000-05:00"/>
   <c:directory name="calabash-0.8.5/lib/" date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="389650"
           size="407421"
           name="calabash-0.8.5/lib/calabash.jar"
           date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="1237"
           size="2493"
           name="calabash-0.8.5/README"
           date="2008-11-04T19:29:20.000-05:00"/>
   <c:directory name="calabash-0.8.5/xpl/" date="2008-11-04T19:29:20.000-05:00"/>
   <c:file compressed-size="175"
           size="255"
           name="calabash-0.8.5/xpl/pipe.xpl"
           date="2008-11-04T19:29:20.000-05:00"/>
</c:zipfile>
```
