# Generating an `accessibility.txt` File (Optional)

In July 2023, **Bogdan Cerovac** proposed an `accessibility.txt` file,
similar to `security.txt`, intended for the website root.
See his proposal [Accessibility.txt – a proposed standard which allows websites to define accessibility policies](https://cerovac.com/a11y/2023/07/accessibility-txt-a-proposed-standard-which-allows-websites-to-define-accessibility-policies/)

It includes human-readable fields such as:

-   Contact information
-   Expiration date
-   Preferred languages
-   Link to the accessibility statement
-   Stated WCAG conformance
-   Last update date

### This project recommends generating `accessibility.txt` *automatically* from `accessibility.json`.

This keeps a single authoritative source of truth while still providing
a lightweight human-readable version.

Example conversion:

**Input: `accessibility.json`**

``` json
{
  "language": "en",
  "project": {
    "contact": {
      "email": "accessibility@example.org"
    },
    "scope": {
      "languages": ["en", "de"]
    }
  },
  "evaluation": {
    "conformance": "partially_conformant",
    "lastAudit": "2025-11-25",
    "reportURL": "https://example.org/accessibility-statement"
  },
  "generatedAt": "2025-11-27T10:35:00Z"
}
```

**Generated `accessibility.txt`:**

    Contact: mailto:accessibility@example.org
    Preferred-Languages: en, de
    Accessibility-Statement: https://example.org/accessibility-statement
    WCAG-Conformance: partially conformant
    Last-Update: 2025-11-25
    Generated-From: accessibility.json

Recommended locations:

    /accessibility.txt
    /.well-known/accessibility.txt
