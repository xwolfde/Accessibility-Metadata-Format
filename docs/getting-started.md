# Getting Started for Developers

The Accessibility Metadata Format allows developers of plugins, themes, templates, components, and applications to provide a machine-readable accessibility report. Website operators can use these reports to generate or complete their accessibility statements, even if they are not accessibility experts.

This guide explains how developers can implement the format in different environments.

---

## 1. Create an `accessibility.json` File

Every project should contain a file named:

```
accessibility.json
```

This file MUST be placed in the project root.

Example locations:

```
/your-plugin/accessibility.json
/your-theme/accessibility.json
/your-library/accessibility.json
```

---

## 2. Provide a Public Copy (Optional but Recommended)

You MAY also expose a public version of the file at:

```
/.well-known/<component-prefix>-accessibility.json
```

### Important

Because a website may contain multiple components, **the file name MUST include a component prefix**, such as:

- `mytheme-accessibility.json`
- `shoppingcart-accessibility.json`
- `seo-plugin-accessibility.json`

This prevents naming collisions if multiple components expose metadata through `.well-known/`.

Examples:

```
/.well-known/myplugin-accessibility.json
/.well-known/mytheme-accessibility.json
```

---

## 3. Follow the JSON Schema

Use the official schema:

```
schema/v1/accessibility.schema.json
```

You can start from the provided examples:

- `examples/minimal-accessibility.json`
- `examples/full-accessibility.json`

Adapt these templates to your project.

---

## 4. Fill in the Project Information

Include details about:

- project name and version  
- component type (plugin, theme, application, etc.)  
- contact information  
- scope of evaluation  
- legal basis  
- roadmap (optional)

---

## 5. Add Accessibility Evaluation Data

Document:

- standard used (e.g., WCAG 2.2)  
- conformance level  
- issues found  
- limitations  
- test environment (optional)  
- test runs (optional)

---


# CMS-Specific Guides

## WordPress (Themes & Plugins)

1. Place the file inside the plugin/theme directory:

```
wp-content/plugins/<your-plugin>/accessibility.json
wp-content/themes/<your-theme>/accessibility.json
```

2. When exposing via `.well-known`, use:

```
/.well-known/<plugin-prefix>-accessibility.json
```

3. Ensure the file is included in distributed ZIPs.

4. Optional: expose via a REST endpoint.

5. Update the file for every release.

---

## Joomla Extensions

1. Place `accessibility.json` in the root of your extension:

```
/your_extension/accessibility.json
```

2. Ensure Joomla installs the file properly.

3. Expose via `.well-known` using a prefixed name:

```
/.well-known/<extension-prefix>-accessibility.json
```

4. Validate with the schema and update per release.

---

# Frontend Frameworks & Libraries

## React Component Libraries

1. Place `accessibility.json` next to `package.json`.

2. Ensure it is included in the npm package:

```json
"files": [
  "dist/",
  "accessibility.json"
]
```

3. Optionally expose a public `.well-known` file:

```
/.well-known/<package-name>-accessibility.json
```

4. Validate and update on each release.

---

## Vue, Svelte, Angular

Same pattern as React:

- place at project root  
- include in distribution  
- optionally expose via `.well-known/<prefix>-accessibility.json`  
- validate on CI  

---

# Backend Applications (Node/Express)

1. Add the file to the project root:

```
/accessibility.json
```

2. Serve it publicly with a prefixed filename:

```js
app.get('/.well-known/myapp-accessibility.json', function (req, res) {
    res.sendFile(__dirname + '/accessibility.json');
});
```

3. Validate via CI and update with every deployment.

---


## Validate the File

Use AJV:

```bash
ajv validate   -s schema/v1/accessibility.schema.json   -d accessibility.json
```

Or Python:

```python
from jsonschema import validate
import json

with open("schema/v1/accessibility.schema.json") as f:
    schema = json.load(f)

with open("accessibility.json") as f:
    data = json.load(f)

validate(instance=data, schema=schema)
```

Include validation in CI for each release.

---


# Final Notes

- Always use a **prefixed filename** when exposing the metadata under `.well-known/`.
- Always validate your file when publishing a new release.
- Keep your metadata updated and accurate to support website operators in creating complete accessibility statements.
