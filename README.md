# Accessibility Metadata Format

Dieses Repository definiert ein maschinenlesbares JSON-Format zur Beschreibung von Barrierefreiheits-Reports (z.B. WCAG) von Webprojekten, Themes, Templates oder Anwendungen, welche innerhalb von Webangeboten verwendet werden.
Diese Reports sollen als Grundlage dienen, um auf den Webabgeboten die jeweils notwendige Barrierefreheitserklärung erstellen zu können.


## Dateien

- `schema/v1/accessibility.schema.json`  
  JSON Schema für Version 1.0 des Formats.

- `examples/minimal-accessibility.json`  
  Minimales Beispiel mit nur den notwendigen Feldern.

- `examples/full-accessibility.json`  
  Ausführliches Beispiel mit allen aktuell vorgesehenen Feldern.

- `docs/specification-v1.md`  
  Spezifikation der Felder, Typen und Bedeutungen.

## Nutzung

1. Report-Datei im Projekt als `accessibility.json` ablegen.
2. Optional zusätzlich als `.well-known/accessibility-projectname.json` im Webroot bereitstellen.
3. Mit dem JSON Schema aus `schema/v1/accessibility.schema.json` validieren.
