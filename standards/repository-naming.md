# Repository Naming Standard

## Status

**Status:** Approved  
**Applies to:** Repositories governed by GreenStag  
**Policy owner:** GreenStag Governance  
**Canonical public location:** `.github/standards/repository-naming.md`

## Purpose

This standard defines how repositories governed by GreenStag are named.

Consistent repository names improve:

- discoverability
- readability
- automation
- documentation
- dependency management
- long-term governance

Repository names form part of the organisation’s technical vocabulary. Names must therefore be deliberate, stable and predictable.

## Security and information-disclosure boundary

This public standard defines naming rules only.

This document must not contain:

- names of private repositories
- links to private repositories
- private repository descriptions
- private repository visibility
- internal repository inventories
- private product codenames
- private system names
- internal workspace layouts
- local filesystem paths
- private dependency relationships
- internal migration targets
- internal automation details
- connector configuration
- agent configuration
- private ownership or access-control information
- private infrastructure information

Private repository inventories, migration maps, dependency records and implementation plans must be maintained in an appropriately access-controlled governance location.

Examples in this document must be generic, public, fictional or explicitly approved for public disclosure.

## Naming convention

Repository names must use **lowercase kebab-case** unless an approved exception applies.

Kebab-case uses lowercase words separated by hyphens.

### Correct

- `example-service`
- `example-documentation`
- `example-website`
- `example-governance`
- `example-workspace`

### Incorrect

- `example_service`
- `exampleService`
- `Example-Service`
- `example service`
- `EXAMPLE-SERVICE`

## Core rules

Repository names must:

1. use lowercase letters
2. separate words with hyphens (`-`)
3. use clear and descriptive terms
4. remain reasonably concise
5. reflect the repository’s primary responsibility
6. avoid unnecessary abbreviations
7. avoid implementation details likely to become obsolete
8. avoid disclosing confidential information
9. remain stable once adopted

Repository names must not:

1. use underscores (`_`)
2. use spaces
3. use uppercase letters
4. use ambiguous abbreviations
5. expose confidential project, customer, infrastructure or security information
6. use temporary status terms such as `new`, `final`, `latest` or `test` for permanent repositories
7. encode version numbers unless the repository is intentionally version-specific
8. duplicate the responsibility of an existing repository
9. conflict with an established product, capability or organisational concept
10. imply that a repository is public when its existence or purpose is confidential

## Platform-defined exceptions

Names required or conventionally defined by a platform may retain their platform-specific format.

Approved platform-defined exceptions include:

- `.github`

The `.github` repository must retain its platform-defined name because GitHub assigns special behaviour to that name.

Other platform-defined exceptions must be documented through the governance process.

## Prefix conventions

### Organisation prefix

An organisation prefix may be used for repositories representing:

- organisation-wide capabilities
- shared services
- governance assets
- branded organisational assets
- public organisational resources

The approved organisation prefix must be used consistently.

The exact inventory of prefixed repositories must not be published in this standard unless every listed repository is approved for public disclosure.

### Abbreviated prefix

An abbreviated organisation prefix may be used only when:

- the abbreviation is established
- its meaning is unambiguous
- its use has been approved
- it does not expose confidential information

An abbreviated prefix must not be introduced merely to shorten a repository name.

### Unprefixed names

An unprefixed name may be used when the repository represents:

- a distinct public product
- a published specification
- an independently meaningful capability
- an upstream project whose name should be preserved
- a public open-source project with an established identity

An unprefixed name must not be used merely to avoid the approved organisation prefix.

## Repository categories

Repository names should align with the repository’s primary category.

### Organisation and governance

Repositories defining organisational policy, governance, standards or operating structures should use an approved organisational naming pattern.

Public governance repositories must contain only material approved for public disclosure.

Private governance repository names and contents must not be enumerated in this public standard.

### Shared capabilities

Repositories implementing shared organisational capabilities should normally use the approved organisation prefix.

The name should describe the capability without exposing confidential architecture or implementation details.

### Experimentation

Repositories intended for experiments, proofs of concept or disposable technical exploration should indicate that responsibility without revealing confidential project information.

A permanent product should not remain indefinitely within an experimentation repository once the product has acquired an independent lifecycle.

### Public presence

Repositories supporting a public website, public documentation or public organisation profile should use explicit and descriptive names.

Public-facing repository names should be understandable without requiring internal organisational context.

### Products and foundational technologies

Repositories representing independent products or foundational technologies may use the approved product or technology name.

Before using a product name publicly, confirm that:

- the name is approved for public disclosure
- publication does not reveal confidential work
- the name does not conflict with another product
- the name does not create a trademark or branding conflict

### Workspace coordination

Repositories containing workspace orchestration rather than product implementation should state that purpose clearly.

Workspace repositories must not become containers for implementation that belongs in independently governed repositories.

Private workspace repository names and internal layouts must not be published in this standard.

## Private repository naming

Private repositories must follow the same structural naming rules as public repositories:

- lowercase
- kebab-case
- descriptive
- stable
- appropriately prefixed

However, a private repository name must also be assessed for information disclosure.

A private repository name must not unnecessarily reveal:

- unreleased products
- customer identities
- confidential partnerships
- internal security capabilities
- internal infrastructure
- vulnerability information
- acquisition or commercial activity
- personal information
- credentials or secrets
- incident details
- restricted programme names

Where a descriptive name would disclose sensitive information, use an approved neutral identifier and record the full meaning only in access-controlled governance documentation.

## Public references to private repositories

Public content must not name, link to or enumerate private repositories unless publication has been explicitly approved.

This restriction applies to:

- public README files
- public standards
- public issue templates
- public pull-request templates
- public workflow examples
- public organisation-profile content
- public documentation
- public websites
- badges
- release notes
- discussions
- issue comments
- example configuration
- screenshots
- diagrams
- generated documentation

If a public document needs to refer to a private repository, use a generic description such as:

- `the private governance repository`
- `the relevant private service repository`
- `the controlled workspace repository`
- `an access-controlled implementation repository`

Do not use the actual private repository name.

## Repository inventory

The authoritative repository inventory must be maintained separately from this public standard.

The inventory should record, under suitable access control:

- canonical repository name
- previous repository name
- visibility
- repository category
- purpose
- owner
- responsible team
- lifecycle state
- approved naming exception
- migration state
- dependencies
- external integrations
- public-disclosure status

The private inventory, rather than this public document, is the source of truth for repository existence and migration status.

## Existing non-conforming repositories

An existing repository does not become compliant merely because GitHub redirects its previous URL after a rename.

A repository rename is complete only when:

- the repository has the canonical name
- active local remotes use the canonical URL
- active workspace configuration uses the canonical name
- active documentation uses the canonical name
- active automation uses the canonical name
- deployment configuration uses the canonical name
- dependency references use the canonical name
- permitted public references use the canonical name
- private records use the canonical name
- remaining old-name references have been classified

Historical records may retain obsolete names where editing the records would distort the historical record.

Migration evidence for private repositories must remain in access-controlled records.

## Rename procedure

Repository renames must be treated as controlled migrations.

### Before renaming

1. Confirm the canonical target name.
2. Confirm that the target name is available.
3. Confirm that the target name does not disclose confidential information.
4. Identify dependencies and integrations.
5. Search for active references to the existing name.
6. Record the old and new names in the access-controlled migration map.
7. Identify deployment, workflow, package and integration dependencies.
8. Check whether the old name appears in public content.
9. Confirm that the rename does not conflict with another repository.

### During renaming

1. Rename the repository within the appropriate organisation.
2. Confirm that repository visibility remains correct.
3. Confirm that ownership remains correct.
4. Confirm that the default branch remains correct.
5. Confirm that repository metadata remains correct.
6. Confirm that issues, pull requests, releases and discussions remain accessible.
7. Update active local Git remotes.
8. Update active internal references.
9. Update approved public references where applicable.

### After renaming

1. Verify fetch and push operations using the canonical remote.
2. Verify workflows and required status checks.
3. Verify secrets, variables and environments.
4. Verify publishing and custom-domain configuration where applicable.
5. Verify reusable workflow references.
6. Verify package and deployment integrations.
7. Verify approved public links.
8. Verify internal search and retrieval using the canonical name.
9. Search for residual references to the old name.
10. Remove unauthorised public references to private repository names.
11. Record migration evidence in an access-controlled location.

A redirect is a compatibility mechanism, not a substitute for completing the migration.

## Local directory names

Local repository directories should normally use the same name as the corresponding repository.

For example:

- Repository: `example-service`
- Local directory: `example-service`

This alignment reduces ambiguity in:

- workspace configuration
- shell commands
- scripts
- documentation
- automation
- diagnostic output

Local paths and workstation layouts must not be included in public standards, screenshots or examples unless explicitly approved for disclosure.

## Branch names

This document governs repository names, not the complete branch-naming policy.

Where branch names include multiple words, lowercase kebab-case should be preferred unless another approved workflow defines a different convention.

Examples:

- `feature/repository-standards`
- `fix/deployment-configuration`
- `docs/naming-policy`

The default branch should normally be named `main`.

Branch names must not reveal confidential work when visible outside the intended access boundary.

## File and directory names

This document does not impose kebab-case universally across every file and directory.

Platform-defined and ecosystem-defined names must retain their required forms.

Examples include:

- `README.md`
- `CODEOWNERS`
- `CNAME`
- `SECURITY.md`
- `CONTRIBUTING.md`
- `PULL_REQUEST_TEMPLATE.md`
- `ISSUE_TEMPLATE`
- `.github`

Project-specific file and directory conventions should be defined by the relevant repository or language standard.

## Repository templates

Repository templates must implement this policy.

A repository template should:

- explain the repository naming convention
- use generic or public examples
- avoid references to private repositories
- avoid confidential product or system names
- avoid private repository URLs
- avoid internal filesystem paths
- include the required baseline governance files
- include placeholders only where a repository-specific decision is required
- direct maintainers to this standard as the authoritative naming policy
- remind maintainers to assess public-disclosure risk

Templates demonstrate and apply the standard. Templates do not replace this document as the authoritative public policy.

## References in documentation and automation

Active references must use canonical repository names within the appropriate access boundary.

Relevant references may include:

- Markdown links
- README files
- architecture documents
- decision records
- issue templates
- pull-request templates
- CODEOWNERS guidance
- workflows
- reusable workflow references
- badges
- clone instructions
- package metadata
- dependency declarations
- submodule configuration
- release scripts
- deployment scripts
- workspace files
- repository maps
- automation instructions
- generated documentation

Public documentation and automation examples must not expose private repository names or private repository URLs.

## Historical references

Historical records may retain a previous repository name when changing the record would reduce auditability or misrepresent what existed at the time.

Examples may include:

- closed issue discussions
- merged pull-request discussions
- release notes describing a historical state
- archived reports
- migration evidence

Historical records containing private repository names must remain within the appropriate access boundary.

Public historical records must be reviewed for information disclosure before publication.

## External, mirrored and forked repositories

A repository derived from an external upstream project may retain the upstream repository name when retaining the name materially improves:

- upstream traceability
- synchronisation
- contributor understanding
- automation compatibility
- package identity
- maintenance clarity

The exception must be documented.

The access-controlled decision record should include:

- repository identity
- upstream repository
- relationship to upstream
- reason for retaining the name
- responsible owner
- review conditions

Fork or mirror status does not automatically create an exception. The repository must still be reviewed.

## New repository approval

Before creating a repository, confirm:

- the proposed canonical name
- the repository category
- the repository purpose
- the responsible owner
- whether an existing repository already owns the responsibility
- whether the organisation prefix is required
- whether an exception is being requested
- whether the repository should be public or private
- whether the name itself exposes confidential information
- whether the repository template applies
- whether references to the repository may appear publicly

A repository must not be created under a temporary underscore-form name with the intention of correcting it later.

## Public repository review

Before making a repository public, review:

- repository name
- description
- topics
- README
- commit history
- branches
- tags
- releases
- issues
- pull requests
- discussions
- Actions logs
- workflow files
- badges
- screenshots
- diagrams
- dependency references
- submodules
- generated documentation

The review must identify and remove references to:

- private repositories
- private repository URLs
- confidential systems
- internal paths
- credentials
- secrets
- private infrastructure
- non-public products
- restricted organisational information

Changing repository visibility must be treated as a security-relevant governance action.

## Exceptions

Exceptions must be:

- explicit
- justified
- documented
- approved through the governance process
- limited to the specific repository and reason
- stored within the appropriate access boundary
- reviewed when the underlying constraint changes

An exception must not silently become a general precedent.

## Compliance

A repository is compliant when:

- the repository name follows this standard or has an approved exception
- the repository name does not unnecessarily disclose confidential information
- active references use the canonical name
- public material does not expose private repository information
- local workspace mappings use the canonical name
- documentation uses the canonical name within the appropriate access boundary
- automation uses the canonical name
- migration evidence is recorded where a rename occurred

## Ownership and review

GreenStag Governance owns this standard.

Changes to this standard require:

1. a documented proposal
2. an explanation of the problem being solved
3. an assessment of affected repositories and automation
4. an information-disclosure assessment
5. governance review
6. updates to templates and related documentation where required

## Core principles

> Repository names are durable organisational identifiers. Choose them deliberately, document them appropriately, and migrate them completely.

> Public standards define public rules. Private topology remains private.