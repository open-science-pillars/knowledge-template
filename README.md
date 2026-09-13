# knowledge-template

A conformant Open Knowledge Format (OKF) bundle to copy when starting a
new knowledge bundle, with four annotated example concepts (a dataset,
a gotcha, a recipe, a convention). Conformance target: OKF v0.2
(github.com/GoogleCloudPlatform/knowledge-catalog; the exact text the
organization conforms to is vendored in the marketplace repository
under docs/upstream) plus the Open Science Pillars requirements of the
specification's knowledge layer (docs/SPECIFICATION.md in
open-science-pillars/marketplace). The words used on this page (bundle,
concept, steward, provider bundle) are defined in the
[glossary](https://github.com/open-science-pillars/marketplace/blob/main/GLOSSARY.md).

## From copy to gated

1. **Copy the repository.** Create the new repository from this one in
   a workspace that also holds a checkout of
   [nasa-daac-knowledge](https://github.com/open-science-pillars/nasa-daac-knowledge)
   (the checkers) and
   [build-kit](https://github.com/open-science-pillars/build-kit)
   beside it, the way the gate lays them out.
2. **Rename.** Set `repository.name` in `.osp/repository.yaml` (a copy
   fails `osp.py validate` until it is no longer `knowledge-template`),
   the bundle name in the title of `knowledge/index.md` and
   `knowledge/log.md`, and the release tag pattern in
   `.github/workflows/bundle-gate.yml` to `<name>--v*`. A bundle that
   ships as a plugin adds `.osp/package.yaml` (the marketplace
   repository's
   [package authoring guide](https://github.com/open-science-pillars/marketplace/blob/main/docs/package-authoring-guide.md)).
3. **Delete the four example concepts** (`knowledge/datasets/`,
   `gotchas/`, `recipes/`, `conventions/`, one `example-*` file each)
   once you have real ones, and keep `index.md` and `log.md` current
   as concepts land.
4. **Run the checkers.** Before every pull request, from the
   repository root:
   `uv run ../nasa-daac-knowledge/tools/check_okf_v02.py knowledge/`
   for conformance and `uv run ../build-kit/scripts/osp.py validate .`
   for the metadata. The four examples pass the checker with 0 errors;
   the warnings it reports on them (unverified tier) are what any draft
   shows until a steward signs.
5. **Open the first pull request.** `.github/workflows/bundle-gate.yml`
   runs on every pull request and on main: the canonical metadata
   validates (`osp.py validate`), the bundle conforms to OKF v0.2
   (`check_okf_v02.py`), every script's PEP 723 header covers what it
   imports (`check_script_deps.py`), the wording rules hold
   (`check_prose.py`: specification rules cited by name, no program
   bookkeeping, no em or en dashes) and the signature debt is reported
   (`signature_check.py`, the merge-then-sign rule); a release tag
   enforces zero debt. Lint with the knowledge-linter agent (core
   plugin) before every release.

## What a bundle is

A directory of markdown files under `knowledge/`. One concept per file;
the path is the concept's identity. `index.md` at the bundle root (and
per large subdirectory) lists every concept; `log.md` records change
history. Concepts cross-link with standard markdown links; every gotcha
links its dataset concept.

## Concept types

The specification's concept types section (docs/SPECIFICATION.md in
open-science-pillars/marketplace) defines them, with the required
extras of each:

- `dataset`: identity, access, structure, versions and uncertainty of
  one product.
- `dataset-gotcha`: one trap, its mechanism, its wrong-result mode and
  the correct approach; a high severity requires a matching eval case.
- `recipe`: a validated analysis pattern with inputs, expected values
  and expected-uncertainty ranges.
- `computation`: one attested computation, its sanctioned code identity,
  manifested inputs and the receipt of one run.
- `convention`: a cross-cutting practice.
- `finding`: one falsifiable scientific claim bound to its receipts,
  validity adjudication and confrontation.
- `dead-end`: one attempt that failed, who observed it and what would
  reopen it.
- `field-state`: the positions a field holds on one question as of a
  date, without adjudicating.
- `connector`: the facts about an external service (endpoint,
  transport, tool surface, auth boundary, deprecation status), from
  the specification's connectors section.
- `requirement`: a cross-archive metadata rule, its class and how it is
  checked, as the ESDIS bundle in nasa-daac-knowledge carries them.

This template carries four annotated examples, one each of `dataset`,
`dataset-gotcha`, `recipe` and `convention`; the provider bundles in
nasa-daac-knowledge carry live examples of the rest. How to write a
concept (frontmatter, sources, status, the steward's signature, the
rule that concepts state facts and never instruct the agent) is the
marketplace repository's
[docs/contributing-knowledge.md](https://github.com/open-science-pillars/marketplace/blob/main/docs/contributing-knowledge.md),
and what the checker demands, warning by warning, is
[docs/okf-conformance.md](https://github.com/open-science-pillars/marketplace/blob/main/docs/okf-conformance.md).

## Layout

```
your-repo/
├── README.md · LICENSE · CITATION.cff
├── CODEOWNERS              # stewards of /knowledge/
├── .osp/
│   ├── repository.yaml     # kind, status, spheres, discipline; rename before it validates
│   └── governance.yaml     # maintainers, review policy
├── .github/workflows/bundle-gate.yml  # conformance and signature debt, as CI
└── knowledge/              # the bundle root
    ├── index.md            # okf_version frontmatter; every concept listed
    ├── log.md              # change history, newest first, ISO dates
    ├── datasets/           # example: datasets/example-dataset.md
    ├── gotchas/            # example: gotchas/example-gotcha.md
    ├── recipes/            # example: recipes/example-recipe.md
    └── conventions/        # example: conventions/example-convention.md
```

License: Apache-2.0. Cite via [CITATION.cff](CITATION.cff).
