# Proposal for an XML parse step

The following declaration is for an XML parse step. An XML parse step takes a text/plain input (a sequence of characters) and parses it with an XML parser.

````
<p:declare-step type="p:xml-parse">
   <p:input port="source" primary="true" content-types="text/plain"/>
   <p:output port="result" primary="true"/>
   <p:output port="report" sequence="true"/>
   <p:output port="validation-attempted" sequence="true"/>
   <p:option name="dtd-validate" select="'false'" as="xs:boolean"/>
</p:declare-step>
````

The semantics of the `p:xml-parse` step are that the `source` document is taken as a sequence of characters and parsed with an XML parser. If `dtd-validate` is `true` then a validating parser must be used. If `dtd-validate` is false, validation errors must not be fatal.

If `dtd-validate` is `true` and the document is not valid according to its DTD or if the sequence of characters that appears on the `source` port does not represent a well-formed XML document, an error is raised.

ISSUE: In the case where this error is caught by `p:catch` (how) can the `validation-attempted` and `report` steps be read?

If an error is not raised, the parsed document appears on the `result` port. A report of warnings (or validation errors in the case where `dtd-validate` is `false`) may appear on the `report` port. The step may indicate whether or not DTD validation was attempted on the `validation-attempted` port. (These additional ports exist for consistency with the proposed `p:validate` step.)
