# Accessibility Metadata Format – Spezifikation v1.0

## Einleitung

Dieses Dokument beschreibt das JSON-Format zur Speicherung von Metadaten über
Barrierefreiheitsprüfungen (z.B. WCAG) von Webprojekten und Komponenten.

Die formale Definition befindet sich in `schema/v1/accessibility.schema.json`.

## Struktur

```json
{
  "specVersion": "1.0.0",
  "generatedAt": "2025-11-27T10:35:00Z",
  "language": "de",
  "project": { ... },
  "evaluation": { ... }
}
```

## Felder

### Top Level

`specVersion` – Version des Metadatenformats (z.B. 1.0.0).

`generatedAt` – (optional) ISO-8601 Zeitstempel der Generierung.

`language` – Sprache der Freitexte im Report (BCP47, z.B. de, en).

### `project`

Beschreibt das bewertete Projekt/Produkt.

Wichtige Felder unter `project`:

 - `name` (string, required)

- `version` (string, required)

- `contact.email` (string, required)

- `scope.coverage` (string, required)

- `scope.legalBasis[]` (array of string, required)

Weitere optionale Felder: `id`, `type`, `platform`, `platformVersion`, `homepage`, `repository`, `license`, `lastChange`, `contact.*`, `roadmap.*`.

### `evaluation`

Beschreibt die konkrete Bewertung nach einem bestimmten Standard.

Wichtige Felder:

- `standard` (string, required, z.B. WCAG)
- `version` (string, required, z.B. 2.2)
- `conformance` (string, required)
- `issues[]` (array, required)

Optionale Details: `firstAudit`, `lastAudit`, `method`, `auditor`, `reportURL`, `tests`, `limitations`.

### `issues`

Jedes Issue verweist auf ein Kriterium und beschreibt den Mangel.

Pflichtfelder:

- `criterion` (string, z.B. 1.4.3)
- `reason` (string)
- `level` (z.B. A, AA)

Optionale Felder:

- `alternatives[]` (alternative Zugangsmöglichkeiten)

### `roadmap`

Unter `project.roadmap` können geplante Maßnahmen dokumentiert werden.
Jeder Eintrag kann optional eine issueURL zu einem Issue-Tracker enthalten.

...

(Details hier nach Bedarf weiter ausformulieren.)


## `schema/v1/accessibility.schema.json`

```json
"xwolfde: "https://github.com/xwolfde/accessibility-metadata-format/raw/main/schema/v1/accessibility.schema.json"
```