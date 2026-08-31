# CODEOWNERS Standard

## Status

**Status:** Approved baseline  
**Applies to:** Repositories governed by GreenStag  
**Policy owner:** GreenStag Governance  
**Canonical public location:** `.github/standards/codeowners.md`

## Purpose

This standard defines how GreenStag repositories use GitHub CODEOWNERS files.

CODEOWNERS provides a machine-readable mapping between repository paths and the GitHub users or teams responsible for reviewing changes to those paths.

The objectives are to:

- establish clear review ownership
- request appropriate reviewers automatically
- protect governance and automation files
- reduce ambiguity during pull-request review
- support repository-specific ownership
- create a consistent review-control baseline

CODEOWNERS does not replace:

- repository ownership
- GitHub permission management
- branch protection or repository rulesets
- delivery roles
- governance authority
- security review
- release approval
- documented responsibility boundaries

## Security and information-disclosure boundary

Public CODEOWNERS policy and examples must not disclose:

- private repository names
- private repository topology
- internal team structures not approved for publication
- private GitHub usernames
- confidential products or projects
- internal filesystem paths
- private infrastructure
- customer information
- credentials or secrets

Private repositories may contain repository-specific ownership mappings within their own access boundary.

Public repositories must use only owners and teams whose association with the repository is suitable for public disclosure.

## Required location

Each governed repository should store its CODEOWNERS file at:

`.github/CODEOWNERS`

This standard uses one canonical location to minimise ambiguity.

A repository must not contain competing CODEOWNERS files in multiple recognised locations.

## Repository-specific scope

CODEOWNERS is repository-specific.

The CODEOWNERS file stored in the organisation’s `.github` repository applies to that repository only. It does not automatically define ownership for other repositories.

Each governed repository must contain its own `.github/CODEOWNERS` file unless an approved exception applies.

## Baseline ownership

Every CODEOWNERS file must define a default owner for the complete repository.

Example:

```text
* @approved-owner
```

The default rule ensures that every path has an owner, including files not covered by a more specific rule.

Repository-specific rules may then override the default for particular paths.

## Owner requirements

A CODEOWNERS entry may reference:

- an individual GitHub user
- a visible GitHub organisation team
- multiple eligible users or teams

Every listed owner must have the repository access required by GitHub for CODEOWNERS.

Before adding an owner:

1. verify that the account or team exists
2. verify that the owner has appropriate repository access
3. verify that public disclosure is acceptable
4. verify that the owner accepts the responsibility
5. verify that the ownership mapping reflects actual authority

Do not list:

- inactive accounts
- placeholder accounts
- unknown users
- invisible teams
- teams without suitable repository access
- automation identities that cannot perform review
- workforce identities without an eligible GitHub account
- accounts merely to make the file appear complete

## Initial ownership model

Until repository-specific GitHub teams have been approved and configured, repositories may use the organisation owner or designated maintainer as the default code owner.

This is a transitional baseline.

As the organisation grows, ownership should move from a single individual to appropriate visible GitHub teams where this improves:

- resilience
- separation of duties
- maintainability
- review quality
- organisational continuity

A team must not be placed in CODEOWNERS until its GitHub existence, visibility, membership and repository access have been verified.

## Pattern ordering

CODEOWNERS rules are evaluated in file order.

Place:

1. the broad default rule first
2. more specific path rules afterwards

Later matching rules take precedence over earlier matching rules.

Example:

```text
* @approved-owner
/docs/ @approved-documentation-team
/.github/ @approved-governance-team
```

## Recommended protected paths

Repositories should consider explicit ownership for:

- `/.github/`
- `/docs/`
- `/src/`
- `/tests/`
- deployment configuration
- infrastructure configuration
- dependency manifests
- security-sensitive configuration
- release configuration
- governance files

Specific patterns should be added only where responsibility is real and the referenced owner is eligible.

Do not add decorative ownership rules that do not correspond to an actual review responsibility.

## Governance and automation files

Changes to repository governance and automation should have explicit ownership where practical.

Relevant paths may include:

```text
/.github/
/.github/workflows/
/.github/CODEOWNERS
/SECURITY.md
/CONTRIBUTING.md
/PULL_REQUEST_TEMPLATE.md
```

Repositories may use the default owner for these files until an appropriate governance or security team exists.

## Documentation ownership

A repository may define specific ownership for documentation where a suitable owner exists.

Example:

```text
/docs/ @approved-documentation-owner
*.md @approved-documentation-owner
```

Do not add a documentation-specific rule if the same default owner is responsible for all repository content. Redundant rules increase maintenance without changing behaviour.

## Source and test ownership

Product or implementation repositories may define separate source and test ownership where responsibilities differ.

Example:

```text
/src/ @approved-implementation-team
/tests/ @approved-quality-team
```

Do not model conceptual workforce roles as GitHub teams unless corresponding visible GitHub teams actually exist and have suitable repository access.

## Multiple owners

A pattern may specify more than one eligible owner.

Example:

```text
/security-sensitive-path/ @approved-maintainer @approved-security-team
```

Use multiple owners where:

- responsibilities overlap
- continuity requires more than one reviewer
- specialist review is appropriate
- a transition between owners is underway

Do not add multiple owners merely to increase the apparent strength of the control.

## CODEOWNERS and branch protection

CODEOWNERS identifies and requests appropriate reviewers for matching changes.

Mandatory code-owner approval requires branch protection or a repository ruleset configured to require code-owner review.

A repository must not claim that CODEOWNERS approval is mandatory unless the corresponding GitHub protection setting has been enabled and verified.

The implementation sequence is:

1. create and validate `.github/CODEOWNERS`
2. verify every listed owner is eligible
3. open a test pull request
4. verify the expected owner is requested
5. configure branch protection or a repository ruleset
6. require code-owner review where appropriate
7. verify the merge control using a test pull request

## Default-branch requirement

The CODEOWNERS file must exist on the base branch of a pull request for GitHub to use it for review requests.

The governed baseline should be committed to the repository’s default branch.

Repositories using a non-standard default branch must record that branch in the private repository inventory.

## Forks and mirrors

Forked or mirrored repositories require review before applying GreenStag CODEOWNERS.

Consider:

- the upstream contribution workflow
- the ability to synchronise upstream changes
- an existing upstream CODEOWNERS file
- local modifications
- package and release ownership
- whether GreenStag maintains a divergent implementation

An upstream CODEOWNERS file must not be silently replaced without assessing its purpose.

A GreenStag-specific fork may add or modify ownership where the local maintenance responsibility is explicit.

## Experimental repositories

Experimental repositories should still have a default owner.

A minimal experimental CODEOWNERS file may contain only:

```text
* @approved-owner
```

Additional path-specific rules are unnecessary unless distinct responsibilities already exist.

Experimental status is not a reason to leave ownership undefined.

## Generated and vendored content

Generated or vendored content may be assigned to the repository maintainer or another responsible owner.

CODEOWNERS does not determine whether generated content should be manually edited.

Any restriction on editing generated or vendored content must be documented separately.

## Change control

Changes to `.github/CODEOWNERS` affect repository review routing and may affect merge enforcement.

A change to CODEOWNERS must therefore be treated as a governance-relevant change.

Before merging a CODEOWNERS change:

1. verify the referenced accounts and teams
2. verify repository access
3. verify pattern coverage
4. check for unintended overrides
5. check public-disclosure impact
6. confirm that critical paths retain an owner
7. test the resulting review assignment where practical

## Validation

A CODEOWNERS implementation is verified when:

- `.github/CODEOWNERS` exists on the default branch
- the file has valid CODEOWNERS syntax
- a default `*` rule exists
- every listed user or team exists
- every listed owner has suitable repository access
- public disclosure is acceptable
- expected owners are requested on a test pull request
- protected-branch or ruleset integration is configured where required
- repository-specific exceptions are documented

## Exceptions

A repository may omit CODEOWNERS only through an explicit governance exception.

The exception must record:

- repository identity
- reason
- responsible owner
- risk
- compensating control
- review condition
- expiry or reassessment trigger

Repository age, low activity or experimental status alone is not sufficient justification for an undocumented exception.

## Review

Review CODEOWNERS:

- when a repository is created
- when a repository is renamed
- when repository responsibility changes
- when a listed owner leaves or changes responsibility
- when GitHub teams change
- when repository visibility changes
- when branch protection or rulesets change
- before a private repository becomes public
- during periodic governance review

## Minimum baseline

Every governed repository should initially contain:

```text
# Default repository owner
* @approved-owner
```

More specific rules should be introduced only after corresponding responsibilities and eligible GitHub owners have been established.

## GreenStag initial baseline

Until eligible GitHub teams have been created and verified, native GreenStag repositories may use the following transitional baseline:

```text
# GreenStag CODEOWNERS
#
# Default repository ownership.
# Add path-specific owners only after the corresponding GitHub users
# or visible teams have been verified with suitable repository access.

* @agreenstag
```

This transitional baseline must be reviewed when:

- additional maintainers are appointed
- GitHub teams are introduced
- repository responsibilities are separated
- code-owner approval becomes a required merge control
- the repository changes visibility
- the repository is renamed

## Core principle

> Every governed path has an accountable owner, and every ownership rule reflects a real review responsibility.