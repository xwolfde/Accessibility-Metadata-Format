# Using `accessibility.json` to Generate Schema.org JSON-LD

This document explains how to use the Accessibility Metadata Format
(`accessibility.json`) to generate Schema.org JSON-LD, in particular for the
[`WebSite`](https://schema.org/WebSite) type and its accessibility-related
properties.

Schema.org defines several properties on `CreativeWork` (and thus `WebSite`)
that can be used to express accessibility information, such as:  
`accessibilitySummary`, `accessibilityFeature`, `accessibilityHazard`,
`accessMode`, and `accessModeSufficient`.

The `accessibility.json` file provides a structured source of truth for
accessibility evaluations. JSON-LD should typically be **derived** from this
file, not maintained separately.



## 1. Basic Mapping to `WebSite`

A minimal JSON-LD block for a website could look like this:

```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Example Site",
  "url": "https://example.org/",
  "inLanguage": "en",
  "accessibilitySummary": "This website is partially conformant with WCAG 2.2. A detailed accessibility statement is available at https://example.org/accessibility-statement."
}
```

From `accessibility.json` the following fields are typically mapped:

- `project.name` → `WebSite.name`
- site base URL (from configuration) → `WebSite.url`
- `language` → `inLanguage`
- `evaluation.*` → `accessibilitySummary` (combined into human-readable text)
- optionally `project.version` → `version`
- optionally `project.lastChange` → `dateModified`



## 2. Building `accessibilitySummary` from `accessibility.json`

The `accessibilitySummary` property is intended as a human-readable overview of
the accessibility status, aligned with other metadata but written for humans.

You can construct it from:

- `evaluation.standard` and `evaluation.version`  
- `evaluation.conformance`  
- `evaluation.lastAudit`  
- selected `evaluation.issues[]` summaries  
- `evaluation.reportURL`  

Example logic:

- If `evaluation.conformance = "fully_conformant"` and `issues` is empty:  
  > "This website is fully conformant with WCAG 2.2. The last audit was performed on 2025-11-25. A detailed accessibility statement is available at https://example.org/accessibility-statement."

- If `evaluation.conformance = "partially_conformant"`:  
  > "This website is partially conformant with WCAG 2.2. The last audit was performed on 2025-11-25. Known issues include low contrast for some footer links and partially missing visible keyboard focus in the mobile navigation. A detailed accessibility statement is available at https://example.org/accessibility-statement."



## 3. Example: Full JSON-LD Snippet Derived from `accessibility.json`

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Example Theme Demo",
  "url": "https://example.org/",
  "inLanguage": "en",
  "version": "1.2.3",
  "dateModified": "2025-11-26",
  "accessibilitySummary": "This website is partially conformant with WCAG 2.2. The last audit was performed on 2025-11-25. Known issues include low contrast for some footer links (WCAG 1.4.3) and partially missing visible keyboard focus in the mobile navigation (WCAG 2.1.1). A detailed accessibility statement is available at https://example.org/wcag-report.",
  "hasPart": {
    "@type": "WebPage",
    "url": "https://example.org/wcag-report",
    "name": "Accessibility Statement"
  }
}
</script>
```



## 4. Using `accessibilityFeature` and `accessibilityHazard`

Schema.org also defines more granular properties such as
`accessibilityFeature`, `accessibilityHazard`, `accessMode`, and
`accessModeSufficient`.

Examples:

```json
"accessibilityFeature": [
  "alternativeText",
  "structuralNavigation",
  "displayTransformability"
],
"accessibilityHazard": [
  "noFlashingHazard",
  "noSoundHazard"
]
```



## 5. Recommended Workflow

1. Maintain `accessibility.json` as the canonical source of accessibility
   evaluation data.
2. Use a CMS plugin, build script, or CI step to:
   - read `accessibility.json`
   - generate a JSON-LD snippet for `WebSite`
   - inject it into the HTML (e.g. template, head include).
3. Optionally:
   - also generate `accessibility.txt` from the same source,
   - keep the human-readable accessibility statement page in sync with the JSON.
