![Spec Version](https://img.shields.io/github/v/tag/xwolfde/accessibility-metadata-format?label=Spec&sort=semver)
![Schema Version](https://img.shields.io/github/v/tag/xwolfde/accessibility-metadata-format?label=Schema&sort=semver)
![License](https://img.shields.io/github/license/xwolfde/accessibility-metadata-format)
![Status](https://img.shields.io/badge/Status-Draft-orange)

# Accessibility Metadata Format

The **Accessibility Metadata Format** is a machine-readable JSON standard for documenting the accessibility evaluation of web projects, themes, templates, component libraries, or standalone web applications.

This repository contains:

- The official JSON Schema  
- Full and minimal example files  
- Human-readable specification  
- Optional CI validation workflows

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

## Contact

For questions or suggestions regarding the Accessibility Metadata Format, please open an issue in this repository.
