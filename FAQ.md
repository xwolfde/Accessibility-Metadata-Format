# FAQ – Accessibility Metadata Format

## Who is this format useful for?

### Developers and digital agencies
They can document the accessibility status of their software components and products.  
It helps communicate compliance levels and known issues transparently.

### Website owners, project managers, and hosting providers
They can evaluate the accessibility quality of components before deployment.  
The metadata file makes it easier to identify risks, compliance gaps, and upcoming fixes.

### Web editors and content managers
They often have to maintain accessibility statements without performing technical WCAG audits.  
The metadata format provides technical audit results in a clear and structured way.

### Accessibility testers and auditors
They can store and publish results in a consistent standard, reuse them in automated workflows, and reduce manual documentation effort.

## Additional questions

### Does this replace an accessibility statement?
No.  
It provides machine-readable data *used to generate* an accessibility statement.

### Does the presence of this file guarantee compliance?
No.  
It documents the current evaluation status.

### Can this file be generated automatically?
Yes.  
Any testing tool or CI pipeline can generate or update it as long as it follows the schema.

### Can it store partial audits?
Yes.  
Partial audits simply include fewer issues and may be labelled as `partially_conformant`.

### Is the file intended for public access?
It can be public or private.  
Public placement (e.g. in `.well-known`) helps automated tools, scanners, and providers.
