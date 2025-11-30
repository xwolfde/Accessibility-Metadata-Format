# FAQ – Accessibility Metadata Format

## Where can I use it?
The format is system-agnostic and can be used with:

- CMS platforms (WordPress, TYPO3, Drupal, Joomla, etc.)  
- Static site generators  
- Frontend frameworks (React, Vue, Svelte, etc.)  
- Backend-driven applications  
- Standalone design systems and component libraries  



## Who is this format useful for?

### Developers and digital agencies
They can document the accessibility status of their software components and products.  
It helps communicate compliance levels and known issues transparently.
As a web developer and agency developing an entire web relaunch, you can use the accessibility.json to 
keep track of the status of the individual components.

### Website owners, project managers, and hosting providers
They can evaluate the accessibility quality of components before installation, deployment or purchase.  
Using the accessibility.json file, you can compare plugins, themes, and other components with others before 
installation when searching for and selecting them, and thus make a selection based on the results.
When a new component (e.g., a WordPress plugin) is added to an existing website, the accessibility statement 
applicable to the entire website can be easily added to the accessibility.json file of the new component, 
without having to re-evaluate the entire website.
Furthermore, when searching for and selecting new components, one is not limited to nonspecific statements 
such as "Accessibility ready", but can use the accessibility.json file to check which standard accessibility 
was measured according to and which level of conformance was achieved.

### Web editors and content managers
They often have to maintain accessibility statements without performing technical WCAG audits.  
The metadata format provides technical audit results in a clear and structured way for the components they use in their website. 
With this the web editor can put all component statments together to create the accessibility statement for the whole site.

### Accessibility testers and auditors
They can store and publish results in a consistent standard, reuse them in automated workflows, and reduce manual documentation effort.


## Does this replace an accessibility statement?
No.  
It provides machine-readable data *used to generate* an accessibility statement.

## Does the presence of this file guarantee compliance?
No.  
It documents the current evaluation status.

## Can this file be generated automatically?
Yes.  
Any testing tool or CI pipeline can generate or update it as long as it follows the schema.

## Can it store partial audits?
Yes.  
Partial audits simply include fewer issues and may be labelled as `partially_conformant`.

## Is the file intended for public access?
It can be public or private.  
Public placement (e.g. in `.well-known`) helps automated tools, scanners, and providers.

## Can this project generate an `accessibility.txt` file?

Yes.  
The `accessibility.json` file contains all the structured information needed to
create an optional `accessibility.txt` file as proposed by [Bogdan Cerovac](https://cerovac.com/a11y/2023/07/accessibility-txt-a-proposed-standard-which-allows-websites-to-define-accessibility-policies/) in 2023.

The text-based file is useful for quick human inspection, while the JSON file is
the authoritative, machine-readable source.  
We recommend generating `accessibility.txt` automatically from the JSON metadata
to avoid inconsistencies.


## How does this format relate to EARL?

[EARL (Evaluation and Report Language)](https://www.w3.org/TR/EARL10-Schema/) is a W3C framework for expressing
individual test results in a machine-readable way using RDF.  
It is ideal for accessibility testing tools that need to exchange granular
assertion-level data such as “criterion X passed/failed”.

EARL should be used if:

- you are building or integrating automated testing tools
- you need to exchange atomic evaluation results
- you want to represent results in RDF/linked-data ecosystems
- you need maximum semantic precision at the assertion level

EARL does **not** provide:
project metadata, accessibility statements, conformance summaries, contact data,
legal context, or human-friendly reporting.

This format complements EARL by defining those missing parts.

## How does this format relate to ACT Rules?

[ACT Rules](https://www.w3.org/TR/act-rules-format/) define *how* accessibility tests must be structured and described,
ensuring reproducibility across tools.  
They are not a reporting format and they do not define JSON outputs.

Use ACT Rules when:

- you design or implement accessibility test procedures
- you build automated testing tools
- you need deterministic test behaviour

ACT Rules do **not** define:
project-level metadata, reporting structures, conformance summaries, or
accessibility statement information.

This format works alongside ACT Rules by providing a project-level metadata and
report container.

## Should I use EARL or this format?

Use **EARL** if you need:
- granular, assertion-level results  
- interoperability between automated tools  
- RDF/Linked Data compatibility  

Use **this format** if you need:
- a complete accessibility report  
- metadata about the project, legal basis, contact, roadmap  
- a source for accessibility statements  
- easy JSON integration into CMS, CI pipelines, or websites  
- human-readable and machine-readable reporting  

They solve different problems and can be used together.


## Should I use ACT Rules or this format?

Use **ACT Rules** for:
- defining how a test works  
- standardising the testing procedure  
- ensuring reproducibility between tools  

Use **this format** for:
- structuring and publishing the *results* of evaluations  
- describing conformance status  
- documenting issues and planned fixes  
- referencing test environments and audits  


## Can this format be used to generate Schema.org JSON-LD for accessibility?

Yes.

The `accessibility.json` file can be used as the single source of truth to
generate Schema.org JSON-LD, typically using the `WebSite` type and its
accessibility properties (`accessibilitySummary`, `accessibilityFeature`,
`accessibilityHazard`, etc.).

A common pattern is:

- Use `project.name` and the site URL as `WebSite.name` and `WebSite.url`
- Map `language` to `inLanguage`
- Combine `evaluation.standard`, `evaluation.version`, `evaluation.conformance`,
  `evaluation.lastAudit`, `evaluation.issues[]`, and `evaluation.reportURL` into
  a human-readable `accessibilitySummary`
- Optionally map known features/hazards to `accessibilityFeature` and
  `accessibilityHazard` if such information is available

This way, the JSON-LD on the website is always in sync with the underlying
accessibility evaluation stored in `accessibility.json`.

