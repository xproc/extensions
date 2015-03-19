# Proposal for a sort step

The `p:sort` step is modeled on XSLT's `xsl:sort` element. For each `source` document, the string value of the `select` expression is obtained and used as a sort key. The remaining options determine how that key is used to determine the resulting document order.

<p:declare-step type="p:sort">
    <p:input port="source" sequence="true"/>
    <p:output port="result" sequence="true"/>
    <p:option name="select"/> <!-- XPath expression -->
    <p:option name="lang" as="xs:NMTOKEN"/>
    <p:option name="order"/> <!-- { "ascending" | "descending" } -->
    <p:option name="collation" as="xs:anyURI"/>
    <p:option name="stable" as="xs:boolean"/>
    <p:option name="case-order"/> <!-- { "upper-first" | "lower-first" } -->
    <p:option name="data-type"/> <!-- { "text" | "number" | qname-but-not-ncname }> -->
</p:declare-step>

Note that this step cannot be streamed.
