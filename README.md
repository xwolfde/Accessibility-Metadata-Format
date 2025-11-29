![Spec Version](https://img.shields.io/badge/Spec-1.0.0-blue)
![Schema](https://img.shields.io/badge/JSON%20Schema-v1-blueviolet)
![License](https://img.shields.io/github/license/xwolfde/accessibility-metadata-format)
![Status](https://img.shields.io/badge/Status-Draft-orange)

# Accessibility Metadata Format

A machine-readable JSON format to describe the accessibility evaluation
status of web projects, themes, templates, components, applications, or
other digital products.
This format enables developers, auditors, and organizations to document
and share accessibility-related information in a consistent and
structured way.

The format is defined using a JSON Schema and aims to support:

-   automated generation of accessibility documentation
-   integration into CI/CD pipelines
-   CMS plugin consumption
-   transparency for users and project managers
-   easier creation of accessibility statements


## Purpose


The goal of this format is to enable developers and vendors of products, plugins, themes, templates, and other components used in websites to provide a standardized statement about the accessibility of their work.
The JSON-based report supplied through this format can then be used by website operators to complete their legally required accessibility statement. In practice, most website operators are not accessibility experts and therefore cannot reliably assess the technical accessibility of plugins, themes, or other third-party components.

When a website uses multiple plugins or themes, the individual JSON files can be combined to create a general accessibility statement for the entire site. However, it's important to note that these files can only represent the technical accessibility of the results generated or influenced by these components. They cannot assess accessibility issues that may arise from editorial work.

For a complete website test that also examines the results of editorial work, a proper test according to WCAG or other recognized testing standards is necessary.

The format is system-agnostic and can be used with:

- CMS platforms (WordPress, TYPO3, Drupal, Joomla, etc.)  
- Static site generators  
- Frontend frameworks (React, Vue, Svelte, etc.)  
- Backend-driven applications  
- Standalone design systems and component libraries  


## Specification

The formal definition is provided as a JSON Schema:

    schema/v1/accessibility.schema.json

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

-   ajv-cli\
-   python-jsonschema\
-   VS Code JSON Schema integration\
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
