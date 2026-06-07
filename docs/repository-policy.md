# Repository Policy

This repository is the public companion monorepo for Agentique documentation, schemas, starters, local validation tooling, workflow validation, read-only readback helpers, review-only uploader tooling, and release smoke checks.

Source repository, approved npm package registry pages, action usage reference, badge/readback documentation, and `agentique.io` public-link publication are Go because:

- Owner approval exists.
- Public-content review passes.
- Secret scanning passes.
- Support and security routes are reviewed.
- Hosted CI for the latest pushed release candidate passes.
- Branch protection is enabled for long-lived public release maintenance.
- Final repository, package, docs, schema, action usage, badge/readback documentation, and `agentique.io` links are approved.

Package registry pages, badge/readback documentation, and action usage documentation are approved after publication and smoke testing. `@agentique.io/uploader` is published at version `0.2.0` after owner-approved publication, hosted CI evidence, registry readback, and clean install smoke. GitHub Marketplace-style promotion remains a separate future channel.

Parser/variant package changes in the current source branch target `0.2.0` and are Go for the coordinated package-release claim. Registry readback shows schemas, validator, action, readback, and uploader at version `0.2.0`. Owner approval to use the manual GitHub Actions publishing workflow is recorded, and registry install smoke passed.

Public history must remain public-safe. Do not add private planning material, private platform evidence, local workspace paths, generated archives, dependency folders, credentials, or unpublished operational procedures.
