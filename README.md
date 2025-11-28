![Spec Version](https://img.shields.io/badge/Spec-1.0.0-blue)
![Schema](https://img.shields.io/badge/JSON%20Schema-v1-blueviolet)
![License](https://img.shields.io/github/license/xwolfde/accessibility-metadata-format)
![Status](https://img.shields.io/badge/Status-Draft-orange)

# Accessibility Metadata Format

The **Accessibility Metadata Format** is a machine-readable JSON standard for documenting the accessibility evaluation of web projects, themes, templates, component libraries, or standalone web applications.

The goal of this format is to enable developers and vendors of products, plugins, themes, templates, and other components used in websites to provide a standardized statement about the accessibility of their work.
The JSON-based report supplied through this format can then be used by website operators to complete their legally required accessibility statement. In practice, most website operators are not accessibility experts and therefore cannot reliably assess the technical accessibility of plugins, themes, or other third-party components.

When a website uses multiple plugins or themes, the individual JSON files can be combined to create a general accessibility statement for the entire site. However, it's important to note that these files can only represent the technical accessibility of the results generated or influenced by these components. They cannot assess accessibility issues that may arise from editorial work.

For a complete website test that also examines the results of editorial work, a proper test according to WCAG or other recognized testing standards is necessary.

This repository contains:

- [The official JSON Schema](schema/v1/accessibility.schema.json)  
- [Human-readable specification](docs/specification-v1.md)  
- [Developer documentation](docs/getting-startet.md)
- [Frequently asked questions.](FAQ.md)
- Example files  
Frequently Asked Questions.

---

## Purpose

This format enables:

- **Automated generation of accessibility statements**  
- **Consistent documentation of WCAG/EN 301 549 compliance**  
- **Machine-readable accessibility metadata for CMS/plugins/tools**  
- **Improved transparency for third-party themes and components**  
- **Integration into CI/CD pipelines to ensure ongoing compliance**

The format is system-agnostic and can be used with:

- CMS platforms (WordPress, TYPO3, Drupal, Joomla, etc.)  
- Static site generators  
- Frontend frameworks (React, Vue, Svelte, etc.)  
- Backend-driven applications  
- Standalone design systems and component libraries  

---

## Further Information

See the [FAQ](FAQ.md) for additional details.

---

## File Structure

### The accessibility report

A project should provide an accessibility metadata file named:

```
accessibility.json
```

This file SHOULD be placed in the project root and MAY also be served at:

```
/.well-known/accessibility.json
```

### The JSON Schema

The schema for version 1.0 is located at:

```
schema/v1/accessibility.schema.json
```

### Documentation

The full formal specification is located at:

```
docs/specification-v1.md
```

### Example Files

This repository contains:

```
examples/minimal-accessibility.json
examples/full-accessibility.json
```

---

## Repository Structure

```
accessibility-metadata-format/
├── README.md
├── LICENSE
├── schema/
│   └── v1/
│       └── accessibility.schema.json
├── docs/
│   └── specification-v1.md
└── examples/
    ├── minimal-accessibility.json
    └── full-accessibility.json
```

---

## Usage

### Validate an accessibility.json file using AJV

```bash
ajv validate   -s schema/v1/accessibility.schema.json   -d accessibility.json
```

### Validate using Python

```python
from jsonschema import validate
import json

with open("schema/v1/accessibility.schema.json") as f:
    schema = json.load(f)

with open("accessibility.json") as f:
    data = json.load(f)

validate(instance=data, schema=schema)
```

---

## Versioning

The metadata format follows semantic versioning for its **schema**:

- **MAJOR**: Breaking changes  
- **MINOR**: Backwards-compatible additions  
- **PATCH**: Corrections or clarifications  

Each major version is stored under its own directory:

```
schema/v1/
schema/v2/
...
```

---

## License

Depending on your repository policy, this project may be published under  **CC BY 4.0** 

---

## Contributing

Pull requests and proposals for improvements to the format, schema, or documentation are welcome.  
Please ensure changes remain backwards-compatible within a major version and include updated examples where required.

---


# Author

**Wolfgang Wiese**  
Web Accessibility Specialist, Regional Computing Center (RRZE)  
Friedrich-Alexander-Universität Erlangen-Nürnberg  
GitHub: [@xwolfde](https://github.com/xwolfde)
Bluesky: [@xwolf.de](https://bsky.app/profile/xwolf.de) 
Contact: <wolfgang.wiese@fau.de>

> Opinions expressed in this project are my own and do not necessarily represent the views of the university.



## Contact

For questions or suggestions regarding the Accessibility Metadata Format, please open an issue in this repository.
