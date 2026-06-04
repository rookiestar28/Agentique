# Package Release Provenance

Companion packages are released under the `@agentique.io` npm scope after owner review and registry readback.

## Publishable Packages

- `@agentique.io/schemas` at version `0.1.0`
- `@agentique.io/validator` at version `0.1.0`
- `@agentique.io/action` at version `0.1.0`
- `@agentique.io/readback` at version `0.1.0`
- `@agentique.io/uploader` source package at version `0.1.0`; npm publication pending owner-approved closeout

Schemas, validator, action, and readback are public on npm. Uploader is implemented in source and included in package dry-run checks, but registry readback currently reports it as not found.

## Required Pre-Publish Checks

- Package tests pass.
- Package production dependency audits pass.
- `npm run pack:dry-run` passes.
- Release manifest and public-content checks pass.
- Release notes are reviewed for private data, local paths, unsupported claims, and package scope accuracy.
- Final public repository and package URLs are approved.
- Public release notes mention surfacing contracts, lane descriptors, uploader source status, and read-only helper support only as baseline companion metadata.

## Provenance Posture

Use registry trusted publishing where available. Trusted publishing uses CI identity instead of long-lived package tokens and can publish provenance attestations for packages.

The checked-in package publishing workflow is manual-only, uses GitHub OIDC with `id-token: write`, does not reference repository secrets, and passes `--provenance` explicitly to each `npm publish` command. The npm organization/package owner must still configure the matching Trusted Publisher entry in npm before the workflow can publish without a token.

Provenance helps consumers trace package source and build context. It does not mean a package is risk-free, platform-approved, or safety-certified.

The first public package publication used an owner-approved short-lived granular token fallback after local and hosted validation passed. Future releases should prefer the checked-in GitHub Actions trusted-publishing workflow once npm Trusted Publisher setup is complete. Token fallback is a contingency for owner-approved manual recovery only; it is not part of the normal trusted-publishing workflow and must not be added to workflow YAML.

Registry readback and clean install smoke passed with npm 11.14.1 for the published dotted `@agentique.io` package set. Uploader requires separate registry readback and install smoke before its package page is advertised.

Local release candidates should run:

```bash
npm run registry:readback
npm run install:smoke
```

The registry readback script records the current expected state: schemas, validator, action, and readback are published, while uploader remains pending until owner-approved publication.

Current uploader publication closeout is No-Go. Do not advertise `@agentique.io/uploader` as installable until owner approval, hosted CI evidence, registry publish/readback, and clean install smoke from npm are recorded.

Public package provenance must not include platform scoring, quarantine criteria, internal review procedures, moderation disposition logic, or operational playbooks.

## Version And Tag Discipline

- Use semver for package versions.
- Keep package versions aligned for coordinated companion releases unless a package has an independent patch.
- Use release tags only after owner approval.
- Do not create public tags for dry-runs.
- Review release notes before publication.

## Publish Step Isolation

The checked-in workflow publishes each package in its own step with an explicit `working-directory`. This makes package-level failure evidence visible in GitHub Actions and avoids hiding partial-publish state inside one shell block.

After any publish failure, compare registry readback for all publish-target packages before advertising, tagging, or changing public URL inventory. If one package version is live while another failed, stop promotion and either publish the missing package version, deprecate the affected version, or publish a coordinated replacement version according to owner review.

## Rollback

If a package release contains incorrect files or wording, stop additional publishing, deprecate or replace the affected package version according to registry policy, and update release notes with a public-safe correction.
