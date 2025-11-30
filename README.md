![Spec Version](https://img.shields.io/badge/Spec-1.0.0-blue)
![Schema](https://img.shields.io/badge/JSON%20Schema-v1-blueviolet)
![License](https://img.shields.io/github/license/xwolfde/accessibility-metadata-format)
![Status](https://img.shields.io/badge/Status-Draft-orange)

# Accessibility Metadata Format

A machine-readable JSON format to document the accessibility status of web components (themes, plugins, components, etc.).
Purpose: Developers and agencies provide standardized metadata for their work; website operators use it for legally required accessibility statements.


## Example

The following example shows a sample accessibility.json file, which would residue in the plugins folder:

```json
{
  "specVersion": "1.0.0",
  "language": "en",
  "project": {
    "name": "Feed Widget Plugin",
    "version": "1.0.0",
    "type": "plugin",
    "platform": "WordPress",
    "platformVersion": "6.5",
    "contact": {
      "email": "support@example.org"
    },
    "scope": {
      "coverage": "feed functionality",
      "includesContent": false,
      "legalBasis": ["WCAG 2.2"]
    }
  },
  "evaluation": {
    "standard": "WCAG",
    "version": "2.2",
    "conformance": "partially_conformant",
    "issues": [
      {
        "criterion": "1.4.3",
        "level": "AA",
        "reason": "Text size contrast fails AA requirements in feed items"
      }
    ]
  }
}

```

This example shows the minimal output for a plugin that only outputs feed content, so evaluation covers only the feed output. 
The text size issue is technical (not editorial content like blog posts).
By seeing this info website operators would combine this with other components' metadata to complete their accessibility statement or chose another plugin without issues.


## Specification

The formal definition is provided as a JSON Schema:

    [schema/v1/accessibility.schema.json](schema/v1/accessibility.schema.json)

This schema describes the full structure of the `accessibility.json`
metadata file, including:

-   Project information
-   Contact details
-   Scope of evaluation
-   Applied accessibility standard (WCAG, EN 301 549, etc.)
-   Conformance status
-   Known issues
-   Limitations
-   Planned improvements
-   Test environment
-   Audit metadata


## Documentation

This repository contains:

- [Getting started](docs/getting-started.md)
- [The official JSON Schema](schema/v1/accessibility.schema.json)  
- [Human-readable specification](docs/specification-v1.md)  
- [Generating an `accessibility.txt` File (Optional)](docs/generating-acessibility-txt.md)
- [Mapping to EARL](docs/mapping-to-earl.md)
- [Schema.org JSON-LD](docs/schema-org-jsonld.md)
- [Frequently asked questions](docs/FAQ.md)
- Example files  

### Folder Structure

    accessibility-metadata-format/
    ├── README.md
    ├── LICENSE
    ├── schema/
    │   └── v1/
    │       └── accessibility.schema.json
    ├── examples/
    │   ├── minimal-accessibility.json
    │   └── full-accessibility.json
    └── docs/
        ├── overview.md
        ├── getting-started.md
        ├── generating-accessibility-txt.md
        ├── specification-v1.md
        ├── mapping-to-earl.md
        ├── schema-org-jsonld.md
        └── FAQ.md



## File Structure

### The accessibility report

A project should provide an accessibility metadata file named:

```
accessibility.json
```

This file SHOULD be placed in the project root and MAY also be served at:

```
/.well-known/<projectname-prefix>-accessibility.json
```

### The JSON Schema

The schema for version 1.0 is located at:

```
schema/v1/accessibility.schema.json
```


## Relation to W3C EARL and ACT Rules

This project does not replace [EARL (Evaluation and Report Language)](https://www.w3.org/WAI/standards-guidelines/earl/) 
or [ACT Rules](https://www.w3.org/TR/act-rules-format/).
Instead, it fills a gap those W3C technologies intentionally leave open.

**ACT Rules** define *how accessibility tests should be written*, including
input conditions, testing procedures, and expected outcomes.  
They do *not* define how accessibility reports should be stored, summarised, or
distributed.

**EARL** is a generic RDF-based framework to represent individual test
assertions in a machine-readable way.  
It is excellent for tools but it does not define:

- project metadata
- conformance summaries
- contact information
- legal bases
- accessibility statements
- roadmaps or planned fixes
- human-oriented reporting

The Accessibility Metadata Format complements both technologies by providing the
*project-level metadata* and *high-level reporting structure* that ACT and EARL
do not cover.  
In short:

- **ACT defines how to test**  
- **EARL defines raw test results**  
- **This format defines the complete accessibility report and project metadata**  


## Validation

Any standard JSON Schema validator can be used:

-   ajv-cli
-   python-jsonschema
-   VS Code JSON Schema integration
-   GitHub Actions (example workflow included)



## License

Depending on your repository policy, this project may be published under  **CC BY 4.0** 



## Contributing

Pull requests and proposals for improvements to the format, schema, or documentation are welcome.  
Please ensure changes remain backwards-compatible within a major version and include updated examples where required.



## Author

**Wolfgang Wiese**  
Head of Web Development & Digital Accessibility, Regional Computing Center (RRZE)  
Friedrich-Alexander-Universität Erlangen-Nürnberg  
GitHub: [@xwolfde](https://github.com/xwolfde)
Bluesky: [@xwolf.de](https://bsky.app/profile/xwolf.de) 
Contact: <wolfgang.wiese@fau.de>

> Opinions expressed in this project are my own and do not necessarily represent the views of the university.



## Contact

For questions or suggestions regarding the Accessibility Metadata Format, please open an issue in this repository.
