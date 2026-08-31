# Branch Protection Standard

## Status

**Status:** Approved baseline  
**Applies to:** Native repositories governed by GreenStag  
**Policy owner:** GreenStag Governance  
**Canonical public location:** `.github/standards/branch-protection.md`

## Purpose

This standard defines the minimum protection required for default branches in repositories governed by GreenStag.

The objectives are to:

- prevent accidental deletion of default branches
- prevent destructive force pushes
- route changes through pull requests
- preserve an auditable change history
- require successful automated validation where reliable checks exist
- allow a solo maintainer to operate without creating an approval deadlock
- provide a controlled path towards stronger review enforcement as additional maintainers become available

Branch protection complements, but does not replace:

- CODEOWNERS
- repository permissions
- pull-request templates
- automated testing
- security review
- governance review
- release controls
- documented repository ownership

## Security and information-disclosure boundary

This public standard must not disclose:

- private repository names
- private repository topology
- private branch names
- internal infrastructure
- confidential workflows
- private status-check names
- deployment environments
- private GitHub usernames
- internal team membership
- credentials or secrets

Repository-specific implementation records must remain within an access boundary appropriate to the repository.

## Scope

This standard applies to native repositories governed by GreenStag.

It does not apply to:

- external-source checkouts
- upstream forks outside GreenStag governance
- mirrors maintained only for synchronisation
- repositories covered by an approved governance exception

A repository does not become governed merely because it is visible within the same GitHub organisation.

## Default branch

The default branch should normally be:

`main`

A repository using another default branch must record the reason in the private repository inventory.

The protection policy must target the repository’s actual default branch.

## Protection mechanism

Use a GitHub repository ruleset where the organisation plan and repository configuration support the required controls.

A classic branch-protection rule may be used where:

- rulesets are unavailable
- a repository already has an appropriate branch-protection rule
- migration to rulesets would provide no immediate governance benefit
- an approved compatibility constraint exists

Do not configure both mechanisms independently without reviewing how the rules interact.

## Solo-maintainer constraint

A repository is operating under the solo-maintainer model when:

- one eligible person performs normal maintenance
- no independent reviewer is consistently available
- no visible GitHub team is available to provide review
- requiring another person’s approval would prevent normal repository operation

Under this model, GreenStag must not configure controls that require an approval the sole maintainer cannot provide.

The solo-maintainer baseline therefore:

- requires pull-request workflow where supported
- requires zero approving reviews
- does not require CODEOWNERS approval
- allows the maintainer to merge the maintainer’s own pull request
- prevents force pushes
- prevents branch deletion
- requires reliable status checks where they exist
- preserves an explicit emergency bypass path where supported

This is a transitional governance state, not a substitute for independent review where independent review becomes practical.

## Baseline ruleset

### Ruleset name

`greenstag-default-branch-baseline`

### Enforcement status

`Active`

Use evaluation mode first if supported and if there is uncertainty about the effect on existing workflows.

Move the ruleset to active enforcement only after validating that normal maintenance remains possible.

### Target

Target the repository’s default branch.

Preferred target:

`Default branch`

If the selected GitHub interface does not provide a default-branch target, target the exact default branch name.

Example:

`main`

Do not target every branch unless the repository has a separately approved requirement for universal branch controls.

## Bypass

Configure a bypass actor only where the selected GitHub plan and ruleset interface support it.

The bypass should be limited to:

- repository administrators
- organisation owners
- an explicitly approved maintainer role
- an approved automation identity where operationally required

Bypass must be used only for:

- emergency recovery
- repairing a broken protection configuration
- resolving an incident where the normal workflow cannot operate
- restoring repository accessibility
- handling an explicitly recorded exceptional condition

Bypass must not become the normal merge workflow.

Where practical, configure bypass as:

`For pull requests only`

This allows an authorised actor to bypass selected rules through an auditable pull request rather than by silently pushing directly to the protected branch.

## Required baseline controls

### Restrict branch deletion

**Enabled**

The default branch must not be deleted through normal repository activity.

Deletion should require explicit administrative or governance action.

### Block force pushes

**Enabled**

Force pushes to the default branch must not be permitted through normal repository activity.

This protects the integrity and continuity of repository history.

### Require a pull request before merging

**Enabled where supported without preventing solo maintenance**

Changes to the default branch should normally be introduced through a pull request.

Pull requests provide:

- a visible change description
- an associated diff
- validation results
- discussion history
- links to issues and decisions
- an auditable merge event

### Required approving reviews

**Set to zero under the solo-maintainer model**

The sole maintainer cannot provide an independent approval for the sole maintainer’s own pull request.

Do not set the required approval count to one until another eligible reviewer is consistently available.

### Require review from CODEOWNERS

**Disabled under the solo-maintainer model**

CODEOWNERS should continue to identify repository ownership.

However, mandatory CODEOWNERS approval must remain disabled while the sole code owner is also the pull-request author.

Enabling mandatory CODEOWNERS approval in that state risks creating a merge deadlock.

### Dismiss stale pull-request approvals

**Disabled under the solo-maintainer model**

This setting has no useful enforcement effect while approving reviews are not required.

Reconsider the setting when independent review becomes mandatory.

### Require approval of the most recent reviewable push

**Disabled under the solo-maintainer model**

This setting requires a person other than the person who made the most recent reviewable push.

Do not enable it until an independent reviewer is available.

### Require conversation resolution before merging

**Enabled**

All unresolved pull-request review conversations must be resolved before merging.

This remains useful for:

- automated review comments
- future external contributions
- bot findings
- maintainer review notes
- later team growth

Resolution must indicate that the finding was:

- addressed
- accepted
- superseded
- transferred to follow-up work
- determined not to apply

Do not resolve a conversation merely to clear the merge control.

### Require status checks to pass

**Enabled only where reliable required checks exist**

A repository should require status checks only when:

- the workflow is present
- the check runs for the relevant pull-request events
- the check is reliable
- the check name is stable
- the check does not depend on unavailable secrets for external pull requests
- the check has completed successfully at least once
- the maintainer knows how to recover from a broken check

Do not select a check merely because it appears in historical workflow data.

Do not require:

- obsolete checks
- experimental checks
- intermittently failing checks
- deployment-only checks that do not run on pull requests
- checks produced by removed workflows
- checks that cannot complete for the expected contribution model

Repositories without reliable automated checks may initially omit required status checks.

The omission must be reviewed when reliable validation is introduced.

### Require branches to be up to date before merging

**Disabled by default**

Requiring a branch to be up to date can create unnecessary update commits and repeated workflow execution for a solo-maintainer repository.

Enable it only when:

- integration risk justifies the additional friction
- the repository receives concurrent pull requests
- the required checks depend materially on the latest default branch
- a merge queue or equivalent workflow is in use

### Block merge when required checks are pending or failing

**Enabled when required status checks are configured**

A configured required check must complete successfully before merge.

Emergency bypass remains the recovery mechanism for a broken required check.

### Require signed commits

**Not required in the initial baseline**

Signed commits may be enabled later through a separate decision.

Do not enable signed-commit enforcement until:

- the maintainer’s signing configuration is verified
- automation identities can comply
- web-based edits can comply
- merge strategies have been tested
- recovery procedures are documented

### Require linear history

**Disabled by default**

Linear history is a repository workflow decision rather than a universal initial protection requirement.

Enable it only where the repository has standardised on:

- squash merging
- rebase merging
- another compatible linear-history workflow

Do not enable it before verifying that the permitted merge methods are compatible.

### Restrict branch creation

**Not applicable to the existing default branch baseline**

Creation restrictions should be handled by a separate branch-naming or repository-governance policy if required.

### Restrict branch updates

**Do not restrict updates solely to a single actor**

The pull-request requirement and status controls provide the intended baseline.

A strict push allow-list may block GitHub Apps, automation, Pages deployment, release workflows or future contributors.

Introduce an allow-list only after identifying every legitimate write actor.

### Lock branch

**Disabled**

A locked branch is read-only and unsuitable for an actively maintained default branch.

## Recommended solo-maintainer configuration

| Control | Initial setting |
|---|---|
| Target | Default branch |
| Enforcement | Active after validation |
| Restrict deletion | Enabled |
| Block force pushes | Enabled |
| Require pull request | Enabled |
| Required approvals | Zero |
| Require CODEOWNERS approval | Disabled |
| Dismiss stale approvals | Disabled |
| Require latest-push approval | Disabled |
| Require conversation resolution | Enabled |
| Require status checks | Enabled only for proven reliable checks |
| Require branch up to date | Disabled by default |
| Require signed commits | Disabled |
| Require linear history | Disabled by default |
| Restrict updates to selected actors | Disabled |
| Lock branch | Disabled |
| Emergency bypass | Enabled for approved administrator or owner where supported |

## Repository classes

### Repository with reliable pull-request checks

Apply:

- prevent deletion
- block force pushes
- require pull requests
- require conversation resolution
- require the proven checks to pass
- zero required approvals
- no mandatory CODEOWNERS approval
- approved administrative bypass

### Repository without automated checks

Apply:

- prevent deletion
- block force pushes
- require pull requests
- require conversation resolution
- zero required approvals
- no mandatory CODEOWNERS approval
- no required status checks
- approved administrative bypass

The absence of automated checks should be recorded as an improvement opportunity, not hidden by selecting an unsuitable check.

### Public configuration or documentation repository

Apply the same baseline.

Before requiring status checks, confirm that the repository has a validation workflow suitable for its content, such as:

- Markdown validation
- YAML validation
- link checking
- issue-form validation
- policy linting

These are examples, not mandatory checks.

### Experimental repository

An experimental repository should still:

- prevent default-branch deletion
- block force pushes
- use pull requests where practical
- preserve an emergency bypass

The repository may omit required status checks if no reliable validation exists.

Experimental status does not justify destructive updates to the default branch.

## Pull-request workflow

The expected solo-maintainer workflow is:

1. create a working branch
2. make the intended changes
3. push the working branch
4. open a pull request
5. complete the pull-request template
6. review the diff
7. confirm that no unintended files are present
8. resolve review conversations
9. wait for required checks
10. merge the pull request
11. delete the working branch where appropriate

The pull request remains useful even without an independent approver because it records:

- intent
- scope
- acceptance criteria
- validation
- governance impact
- security review
- resulting diff
- merge outcome

## Direct pushes

Direct pushes to the default branch should be avoided under normal operation.

Where the configured GitHub plan or repository visibility does not support the desired enforcement, the maintainer should still follow the pull-request workflow voluntarily.

A lack of platform enforcement does not change the documented governance expectation.

## Emergency bypass

Emergency bypass is acceptable only when the normal workflow cannot safely complete.

Examples include:

- a required check is broken because of its own configuration
- a workflow rename leaves a stale required check
- branch protection blocks repair of branch protection
- a deployment incident requires an urgent controlled correction
- repository access or integrity requires recovery

When bypass is used, record:

- the reason
- the change made
- the affected repository
- the validation performed
- any follow-up work
- whether the ruleset requires correction

Do not record confidential incident details in a public repository.

## CODEOWNERS relationship

Each native governed repository must contain:

`.github/CODEOWNERS`

The initial GreenStag baseline assigns default ownership to the designated maintainer.

CODEOWNERS provides ownership metadata and reviewer routing.

Under the solo-maintainer model:

- CODEOWNERS remains required
- automatic review requests may occur
- mandatory code-owner approval remains disabled
- the author may merge after other required controls pass

When another eligible reviewer exists, review this policy before enabling mandatory code-owner approval.

## Transition to multi-maintainer governance

The repository should leave the solo-maintainer model when another eligible maintainer or visible GitHub team is consistently available.

At that point, consider enabling:

- one required approving review
- mandatory CODEOWNERS approval
- dismissal of stale approvals
- approval of the most recent reviewable push by someone other than its author
- restricted review dismissal
- stronger bypass controls
- separation between implementation and approval

Do not enable these controls merely because another account exists.

The additional reviewer must:

- have suitable repository access
- understand the repository
- accept review responsibility
- be available enough to support normal delivery
- be eligible under GitHub’s CODEOWNERS and review rules

## Repository renames

After renaming a repository:

1. confirm the ruleset still targets the intended default branch
2. confirm CODEOWNERS remains on the default branch
3. confirm required checks still report under the expected names
4. confirm GitHub Apps retain access
5. confirm secrets, variables and environments remain correctly scoped
6. confirm Pages and deployment workflows where applicable
7. open a validation pull request
8. verify that the configured merge controls operate
9. update the private migration register

A repository redirect does not prove that governance controls remain correctly attached.

## Validation procedure

Before declaring the baseline complete for a repository:

1. create a temporary working branch
2. make a harmless documentation change
3. push the branch
4. verify that a pull request can be opened
5. verify that direct update controls behave as configured
6. verify that CODEOWNERS identifies the expected owner
7. verify that required checks run
8. verify that a failing required check blocks merge
9. correct the test change
10. verify that successful checks permit merge
11. verify that unresolved conversations block merge
12. resolve the conversation
13. merge the pull request
14. verify that the default branch remains protected
15. record the test result

If the test exposes a lockout or unintended block, use the approved administrative recovery path and correct the ruleset.

## Plan and feature limitations

Branch-protection and ruleset capabilities may depend on:

- repository visibility
- GitHub organisation plan
- repository ownership
- GitHub feature availability

If the required control is unavailable:

1. record the unavailable control
2. record the relevant plan or feature limitation
3. apply all available non-blocking controls
4. retain the documented pull-request workflow
5. identify any compensating control
6. review the limitation if the plan or visibility changes

Do not mark a technical control as implemented when it exists only as documented intent.

## Exceptions

An exception must record:

- affected repository
- unavailable or unsuitable rule
- reason
- risk
- compensating control
- responsible owner
- review condition
- expiry or reassessment trigger

Exceptions must remain within the appropriate information-disclosure boundary.

An external-source checkout outside GreenStag governance does not require an exception because it is outside this policy’s scope.

## Review triggers

Review this standard when:

- another eligible maintainer is appointed
- a visible GitHub review team is created
- the GitHub organisation plan changes
- repository visibility changes
- a repository is renamed
- required workflows change
- a new deployment mechanism is introduced
- CODEOWNERS changes
- a bypass is used
- an enforcement failure occurs
- a protected repository becomes archived
- the contribution model changes

## Compliance

A repository complies with the solo-maintainer baseline when:

- the repository is within GreenStag governance scope
- the default branch is identified
- branch deletion is restricted where supported
- force pushes are blocked where supported
- pull requests are required where supported
- mandatory independent approval is not configured without an eligible reviewer
- reliable required checks are enforced where available
- unreliable or nonexistent checks are not falsely treated as controls
- CODEOWNERS exists at `.github/CODEOWNERS`
- bypass is limited and documented
- the protection has been tested
- limitations and exceptions are recorded

## Core principles

> Protect the branch without locking out the maintainer.

> Pull requests provide an auditable decision point even when independent approval is not yet available.

> Enforcement must reflect the organisation that actually exists, not the organisation the configuration assumes.