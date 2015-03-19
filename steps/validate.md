# Proposal for a generalized validation step

The following declaration is for a generalized validation step. Much of what follows describes how this step applies to XML validation, but the actual validation performed is implementation defined. Validation of JSON data against json-schema would be entirely plausible.

````
<p:declare-step type="p:validate">
   <p:input port="source" primary="true"
            content-types="application/octet-stream"/>
   <p:input port="schema" sequence="true"
            content-types="application/octet-stream"/>
   <p:input port="models" sequence="true"
            content-types="application/xml */*+xml text/*"/>
   <p:output port="result" primary="true" sequence="true"/>
   <p:output port="report" sequence="true"/>
   <p:output port="validation-attempted" sequence="true"/>
   <p:option name="assert-valid" select="'true'" as="xs:boolean"/>
   <p:option name="group" select="''" as="xs:string"/>
   <p:option name="phase" select="''" as="xs:string"/>
   <p:option name="version" as="xs:string"/>
   <p:option name="parameters" as="map(xs:QName,item())"/>
</p:declare-step>
````

The semantics of the `p:validate` step are that the `source` document is validated in an implementation defined way. The `schema` and `models` ports exist only to provide suggestions to the implementation.

There are several possible outputs:

1. If the processor considers that no validation was requested (or does not recognize or cannot perform the requested validation), or if the `assert-valid` option was `false` and validation failed, then the original document is returned on the `result` port.
1. If the processor attempts to validate and succeeds, then the validated document or documents are returned on the `result` port. In this case, the `validation-attempted` port should document the validation or validations that were attempted.
1. If the processor attempts to validate and fails, and the `assert-valid` option is true, then nothing appears on the output port and an error is raised.

ISSUE: In the case where this error is caught by `p:catch` (how) can the `validation-attempted` and `report` steps be read?

The output on the `report` step depends on the validation attempted. For Schematron validation, a report format is defined. For other kinds of validation, the report is implementation-defined.

Although the step is for generalized validation, it does have a couple of options designed to support a specific XML scenario: the XML Model Processing Instruction. In the absense of other information, implementations *should* use the XML Model PI to determine what kind of validation to perform on XML documents.

The `group` and `phase` options provide the corresponding values as discussed in the XML Model PI spec.

The `models` input port and the `validation-attempted` output port use XML documents to describe desired validation in the former case and validations attempted in the latter. The following `c:model` element definition *should* be supported.

````
<c:model
   href? = anyURI
   type? = string
   schematypens? = anyURI
   charset? = string
   title? = string
   group? = string
   phase? = string
   />
````

Additional variations on `c:model` are allowed, as are entirely different vocabulary elements as appropriate.

## Validation with RELAX NG

When RELAX NG validation is selected, the following parameters *should* be recognized: `dtd-attribute-values`, and `dtd-id-idref-warnings`.

# Validation with XML Schema

When XML Schema validation is selected, the following parameters *should* be recognized: `use-location-hints`, `try-namespaces`, and `mode`.

# Validation with NVDL

If an NVDL schema appears on the `models` port, NVDL validation *should* be attempted.
