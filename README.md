# Flatfile Agent Resource System Engineering

<!-- 561-group-standards:badges:start -->
[![Red Cup Engineering](https://img.shields.io/badge/561%20Group-Red%20Cup%20Engineering-c0392b)](https://github.com/red-cup-engineering)
[![License: MIT](https://img.shields.io/badge/license-MIT-c0392b)](LICENSE)
[![Indigenous data: CARE](https://img.shields.io/badge/Indigenous%20data-CARE-4b6f44)](https://github.com/red-cup-engineering/.github/blob/main/GOVERNANCE.md)
[![Tips welcome](https://img.shields.io/badge/tips-welcome-d4a017)](https://github.com/561-group/.github/blob/main/TIPS.md)
<!-- 561-group-standards:badges:end -->

**Shared conformance material for flatfile-based agent resources.** This
engineering section keeps source-qualified identity and record fixtures
used to check that implementations agree on the same identifiers. Its
current executable surface is a checker for those vectors, backed by
the separately maintained
[Flatfile Resource Graph Service](https://github.com/red-cup-engineering/flatfile-resource-graph-service).

This is **not** an agent runtime, a hosted resource graph, or a complete
flatfile installation. The runnable identity implementation lives with
the source owner, not in a copied kernel here.

## Where to begin

The public source in this repository has three relevant parts:

| Path | What it provides |
| --- | --- |
| [Identity vectors](lib/conformance/identity-vectors.json) | Expected identifiers for canonical resource identities |
| [Record vectors](lib/conformance/record-vectors.json) | Expected record-related identifiers |
| [Identity-vector checker](scripts/check-identity-vectors.mjs) | Compare both fixture sets to the current owner's identity implementation |

The checker has one package command, `fars-identity-vectors`. Its Node
entry point is also exposed at the legacy
`./check-identity-vectors` subpath. It produces JSON containing
`owner`, `laws`, `checked`, and `mismatches` and returns a nonzero
exit code if fixtures disagree or cannot be read.

## Running the checks

Use this as part of an installed **engineering workspace** that resolves
`@red-cup-engineering/flatfile-resource-graph-service`, declared here as a
`workspace:*` dependency. The exported
`@red-cup-engineering/flatfile-resource-graph-service/kernel/identity`
implementation is the authority being compared; this checker no longer
requires an eight-level, hard-coded relative path into a specific checkout.

```sh
npm run check   # parse the maintained checker source
npm test        # recompute recorded identity and record vectors
npm run verify  # both checks, with dependencies already resolved
```

The checker accepts an alternative fixture directory containing
`identity-vectors.json` and `record-vectors.json`:

```sh
node scripts/check-identity-vectors.mjs --vectors /path/to/fixture-directory
```

These commands are meaningful only after the owning dependency resolves.
Cloning this section *alone* does not satisfy a `workspace:*` dependency;
no standalone installation is claimed.

## Status and boundaries

The package manifest declares version `0.2.0`. The checked-in fixtures,
source and declared script interface are inspectable now. Successful
conformance requires an executed comparison against a specified version of
the source owner's identity kernel; source files alone are not a passing
result or proof of compatibility with every independent implementation.

The `lib/legacy` and retained logs are historical/context material rather
than additional executable identity providers. Further agent platform
compositions belong to
[Agent Computer Platform System Engineering](https://github.com/red-cup-engineering/agent-computer-platform-system-engineering-services-section).
