# Accessibility Metadata Format — Specification v1.0

Version: **1.0.0**  
Status: **Draft / Public Proposal**  
Authors: *Wolfgang Wiese, University of Erlangen–Nuremberg*  




---

## 1. Introduction

The **Accessibility Metadata Format** defines a machine-readable JSON structure for describing the accessibility evaluation status of a web project, product, theme, template, or standalone web application.

This format is intended to:

- document accessibility compliance (e.g., WCAG, EN 301 549) in a standardized way  
- allow automated generation of accessibility statements (legal requirement in many regions)  
- allow CMS plugins, CI pipelines, or scanners to read structured accessibility info  
- provide verifiable metadata for third-party components (themes, templates, libraries)

The formal definition is included as a JSON Schema:

```text
schema/v1/accessibility.schema.json
```

---

## 2. File Naming and Placement

A typical accessibility report using this format SHOULD be stored as:

```text
accessibility.json
```

The file SHOULD be placed in the project root and MAY additionally be exposed via:

```text
/.well-known/<projectname-prefix>-accessibility.json
```

This allows both local tooling (reading from the project directory) and remote tooling (crawlers, automated checkers) to access the file in a predictable way.

> Please note: The filename /.well-known/accessibility.json should not be used by plugins, themes, or other components. Due to its generic format, this filename should always be reserved for a report for the entire website. Therefore, the project prefix should always be used for components.


---

## 3. Top-Level Structure

A valid accessibility metadata file contains the following top-level structure:

```json
{
  "specVersion": "1.0.0",
  "generatedAt": "2025-11-27T10:35:00Z",
  "language": "en",
  "project": { },
  "evaluation": { }
}
```

### 3.1 Required Top-Level Fields

| Field         | Type     | Required | Description |
|--------------|----------|----------|-------------|
| `specVersion` | string  | yes      | Version of this metadata format (e.g. `1.0.0`). |
| `language`   | string   | yes      | Language of all human-readable text in the file (BCP47, e.g. `en`, `de-DE`). |
| `project`    | object   | yes      | Describes the evaluated project/product. |
| `evaluation` | object   | yes      | Contains the accessibility evaluation data. |

### 3.2 Optional Top-Level Fields

| Field         | Type     | Description |
|--------------|----------|-------------|
| `generatedAt` | string (date-time) | ISO 8601 timestamp of report generation (e.g. `2025-11-27T10:35:00Z`). |

---

## 4. `project` Object

The `project` object describes the software, theme, template, or web application being evaluated.

Example:

```json
"project": {
  "id": "rrze-example-theme",
  "name": "Example Theme",
  "type": "theme",
  "description": "Responsive web theme designed for higher education websites.",
  "platform": "WordPress",
  "platformVersion": "6.7.1",
  "homepage": "https://example.org/example-theme",
  "repository": "https://git.example.org/rrze/example-theme",
  "license": "GPL-2.0-or-later",
  "version": "1.3.7",
  "lastChange": "2025-11-26",
  "contact": { ... },
  "scope": { ... },
  "roadmap": { ... }
}
```

### 4.1 Required Fields in `project`

| Field                    | Type   | Description |
|--------------------------|--------|-------------|
| `name`                   | string | Human-readable project/product name. |
| `version`                | string | Project version (SemVer or equivalent). |
| `contact.email`          | string | Contact email address for accessibility-related issues. |
| `scope.coverage`         | string | Evaluated scope (e.g. `site`, `templates`, `components`). |
| `scope.legalBasis[]`     | array  | List of normative/legal bases used (e.g. `WCAG 2.2`). |

### 4.2 Optional Identification Fields

- `id` — Internal or machine-readable identifier (slug, package name, etc.).  
- `type` — Type of project (e.g. `theme`, `plugin`, `designSystem`, `application`, `website`).  
- `description` — Short human-readable description of the project.

### 4.3 Optional Platform Fields

- `platform` — Underlying platform, e.g. `WordPress`, `TYPO3`, `React`, `Custom`, `None`.  
- `platformVersion` — Version of that platform.

### 4.4 Optional URL and Meta Fields

- `homepage` — Public project/product website URL.  
- `repository` — Source repository URL (e.g. GitHub, GitLab).  
- `license` — License identifier, ideally SPDX (e.g. `GPL-2.0-or-later`, `MIT`).  
- `lastChange` — Date of last relevant project change (YYYY-MM-DD).

---

## 5. Contact Information

The `contact` object describes how users can reach someone regarding accessibility issues.

```json
"contact": {
  "organization": "Regional Computing Center",
  "department": "Webteam",
  "person": "Accessibility Team",
  "email": "accessibility@example.org",
  "phone": "+49 9131 85-12345",
  "url": "https://example.org/contact"
}
```

### 5.1 Required Contact Fields

| Field    | Type   | Description |
|----------|--------|-------------|
| `email`  | string | Contact email address (must be a valid email address). |

### 5.2 Optional Contact Fields

- `organization` — Name of the organization.  
- `department` — Department or unit.  
- `person` — Contact person or role (e.g. “Accessibility Team”).  
- `phone` — Phone number.  
- `url` — URL of a contact or support page.

---

## 6. Scope

The `scope` object describes what is covered by the accessibility evaluation.

```json
"scope": {
  "coverage": "templates",
  "includesContent": false,
  "languages": ["en", "de"],
  "jurisdiction": "EU",
  "legalBasis": ["WCAG 2.2", "EN 301 549", "EAA"]
}
```

### 6.1 Required Scope Fields

| Field        | Type   | Description |
|--------------|--------|-------------|
| `coverage`   | string | High-level coverage of the evaluation (e.g. `site`, `templates`, `components`, `application`). |
| `legalBasis` | array  | List of legal/normative bases used (e.g. `WCAG 2.2`, `EN 301 549`). At least one entry required. |

### 6.2 Optional Scope Fields

- `includesContent` — Boolean. `true` if actual content was evaluated; `false` if only templates/structure/components.  
- `languages[]` — Languages in which the project is typically offered (BCP47 tags).  
- `jurisdiction` — Legal jurisdiction for which this evaluation is relevant (e.g. `EU-DE`, `EU`, `US`).

---

## 7. Roadmap

The `roadmap` object defines planned improvements and future audits.

```json
"roadmap": {
  "plannedImprovements": [
    {
      "description": "Improve link contrast in the footer and sidebar.",
      "relatedCriteria": ["1.4.3"],
      "targetDate": "2026-03-31",
      "issueURL": "https://git.example.org/rrze/example-theme/issues/42"
    }
  ],
  "nextAuditPlanned": "2026-01-31"
}
```

### 7.1 Fields in `roadmap`

| Field                          | Type   | Required | Description |
|--------------------------------|--------|----------|-------------|
| `plannedImprovements[]`        | array  | no       | List of planned remediation actions. |
| `plannedImprovements[].description` | string | yes (per entry) | Description of the planned improvement. |
| `plannedImprovements[].relatedCriteria[]` | array | no | Related criteria (e.g. WCAG numbers). |
| `plannedImprovements[].targetDate` | string (date) | no | Planned completion date. |
| `plannedImprovements[].issueURL` | string (uri) | no | Link to an issue tracker entry. |
| `nextAuditPlanned`            | string (date) | no | Date of the next planned accessibility evaluation. |

---

## 8. Evaluation

The `evaluation` object describes the actual accessibility evaluation in terms of standards such as WCAG.

Example:

```json
"evaluation": {
  "standard": "WCAG",
  "version": "2.2",
  "firstAudit": "2025-10-01",
  "lastAudit": "2025-11-25",
  "method": "thirdParty",
  "auditor": "RRZE Webteam",
  "conformance": "partially_conformant",
  "reportURL": "https://example.org/wcag-report",
  "tests": { ... },
  "issues": [ ... ],
  "limitations": [ ... ]
}
```

### 8.1 Required Evaluation Fields

| Field        | Type   | Description |
|--------------|--------|-------------|
| `standard`   | string | Name of the standard (e.g. `WCAG`, `EN 301 549`). |
| `version`    | string | Version of the standard (e.g. `2.2`). |
| `conformance`| string | Overall conformance status. |
| `issues[]`   | array  | List of identified issues (at least one issue). |

Recommended `conformance` values:

- `fully_conformant`
- `partially_conformant`
- `not_conformant`

### 8.2 Optional Evaluation Fields

- `firstAudit` — Date of first audit under this standard.  
- `lastAudit` — Date of most recent audit.  
- `method` — e.g. `selfAssessment`, `thirdParty`, `automated`.  
- `auditor` — Name of auditor, team or organization.  
- `reportURL` — URL to a more detailed report.  
- `tests` — See next section.  
- `limitations` — See section 10.

---

## 9. Tests

The optional `tests` object describes environment and test runs.

```json
"tests": {
  "environment": {
    "os": "Windows 11",
    "browser": "Firefox 130",
    "assistiveTech": ["NVDA 2023.3"]
  },
  "runs": [
    {
      "type": "automated",
      "tool": "axe-core",
      "version": "4.8.0",
      "date": "2025-11-25",
      "sampleDescription": "Homepage, standard page template, news overview, contact form."
    }
  ]
}
```

All fields inside `tests` are optional in the *format* (you may omit the entire `tests` block), but if present, they must follow the schema.

### 9.1 `environment`

| Field          | Type   | Description |
|----------------|--------|-------------|
| `os`           | string | Operating system used (e.g. `Windows 11`). |
| `browser`      | string | Browser used (e.g. `Firefox 130`). |
| `assistiveTech[]` | array | Assistive technologies used (e.g. `NVDA 2023.3`). |

### 9.2 `runs[]`

| Field             | Type   | Required | Description |
|-------------------|--------|----------|-------------|
| `type`            | string | yes      | Test type (e.g. `automated`, `manual`). |
| `tool`            | string | yes      | Name of the tool or method (e.g. `axe-core`, `expertReview`). |
| `version`         | string | no       | Tool version, if relevant. |
| `date`            | string (date) | yes | Date of the test run. |
| `sampleDescription` | string | no    | Description of the tested sample (pages, flows, etc.). |

---

## 10. Issues

The `issues` array contains all identified accessibility issues.

Example:

```json
"issues": [
  {
    "criterion": "1.4.3",
    "level": "AA",
    "reason": "The contrast ratio of some footer text links is below 4.5:1.",
    "alternatives": [
      {
        "description": "A high-contrast PDF version of the central information is available.",
        "url": "https://example.org/high-contrast-info.pdf"
      }
    ]
  }
]
```

### 10.1 Required Fields per Issue

| Field       | Type   | Description |
|-------------|--------|-------------|
| `criterion` | string | Reference to the relevant criterion, typically a WCAG-style number (e.g. `1.4.3`). |
| `reason`    | string | Explanation why the criterion is not met. |

### 10.2 Optional Fields per Issue

- `level` — Level of the criterion (e.g. `A`, `AA`, `AAA`).  
- `alternatives[]` — Alternative access methods or aids for this issue:

```json
"alternatives": [
  {
    "description": "A high-contrast PDF version of the central information is available.",
    "url": "https://example.org/high-contrast-info.pdf"
  }
]
```

Fields in each `alternative`:

| Field         | Type   | Required | Description |
|--------------|--------|----------|-------------|
| `description`| string | yes      | Description of the alternative solution. |
| `url`        | string (uri) | no | URL to an alternative resource or help. |

---

## 11. Limitations

The `limitations` array describes known non-compliant areas or exceptions.

Example:

```json
"limitations": [
  {
    "area": "Document archive prior to 2018",
    "reason": "archivedContent",
    "description": "Legacy PDF documents may not be fully accessible.",
    "plannedFixDate": null
  }
]
```

### 11.1 Required Fields per Limitation

| Field       | Type   | Description |
|-------------|--------|-------------|
| `area`      | string | Name or description of the affected area (e.g. “archive”, “legacy forms”). |
| `description` | string | Description of the limitation. |

### 11.2 Optional Fields per Limitation

- `reason` — e.g. `archivedContent`, `disproportionateBurden`, `thirdPartyContent`.  
- `plannedFixDate` — Date when the limitation is expected to be resolved, or `null` if not planned.

---

## 12. Schema Validation

The canonical JSON Schema for this format is stored in:

```text
schema/v1/accessibility.schema.json
```

You can validate example files using tools such as **ajv**:

```bash
ajv validate   -s schema/v1/accessibility.schema.json   -d examples/full-accessibility.json
```

Or in Python using `jsonschema`:

```python
from jsonschema import validate
import json

with open("schema/v1/accessibility.schema.json") as f:
    schema = json.load(f)

with open("examples/full-accessibility.json") as f:
    data = json.load(f)

validate(instance=data, schema=schema)
```

---

## 13. Versioning Policy

- This document defines **format version 1.0.0**.  
- Backward-incompatible changes MUST result in a new major version (e.g. `2.0.0`).  
- Backward-compatible, additive changes MAY result in a minor or patch version (e.g. `1.1.0`, `1.0.1`).  

Recommended directory structure:

```text
schema/v1/accessibility.schema.json
schema/v2/accessibility.schema.json
...
```

Each major version MUST have its own schema and specification.

---

## 14. License

The specification and schema MAY be published under: **CC BY 4.0** 

---

_End of Accessibility Metadata Format – Specification v1.0_
