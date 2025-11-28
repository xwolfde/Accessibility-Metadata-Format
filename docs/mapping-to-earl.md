## Mapping to EARL (Evaluation and Report Language)

The Accessibility Metadata Format is higher-level than EARL.  
However, individual entries can be mapped to EARL concepts as shown below.

| Accessibility Metadata Format                     | EARL Concept / Predicate                         | Notes |
|-------------------------------------------------|--------------------------------------------------|--------|
| `evaluation.standard`                             | `earl:test` (with WCAG test definition)         | EARL needs a TestCase resource. |
| `evaluation.version`                              | part of TestCase definition                      | EARL does not store WCAG version directly. |
| `evaluation.issues[].criterion`                   | `earl:test` identifier                           | Must point to WCAG SC URI. |
| `evaluation.issues[].reason`                      | `earl:assertion` → `earl:result` → info          | Stored as human-readable text. |
| `evaluation.issues[].level`                       | Not represented in EARL directly                 | WCAG levels are implicit in SC URIs. |
| `evaluation.issues[].alternatives[]`              | Not covered by EARL                              | Requires extension vocabulary. |
| `evaluation.tests.environment.os`                 | custom metadata outside EARL                     | EARL does not define environment fields. |
| `evaluation.tests.environment.browser`            | idem                                             | |
| `evaluation.tests.environment.assistiveTech[]`    | idem                                             | |
| `evaluation.tests.runs[].type`                    | mapped to EARL Outcome (`earl:passed`, etc.)     | Additional logic needed. |
| `evaluation.tests.runs[].tool`                    | `earl:assertedBy`                                | Tool as Agent. |
| `evaluation.tests.runs[].date`                    | `dct:date` or similar                            | EARL recommends Dublin Core for metadata. |
| `evaluation.conformance`                          | **No direct EARL equivalent**                    | EARL does not define conformance summaries. |
| `project.*`                                       | no equivalent                                    | EARL does not describe projects. |
| `project.contact.*`                               | no equivalent                                    | Must be external metadata. |
| `project.roadmap.*`                               | no equivalent                                    | |
| `limitations[]`                                   | partial mapping via EARL metadata extensions      | Requires external vocabulary. |

### Summary

- **Fully mappable:** individual test results → EARL assertions  
- **Partially mappable:** issue descriptions (mapped to EARL notes)  
- **Not mappable:** project metadata, conformance, roadmaps, limitations, contact info

This demonstrates that both technologies address different layers:

- EARL = *low-level assertions*  
- Accessibility Metadata Format = *high-level accessibility report & metadata*  
