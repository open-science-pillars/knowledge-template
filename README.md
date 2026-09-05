# knowledge-template

A conformant Open Knowledge Format (OKF) bundle to copy when starting a
new knowledge bundle, with one fully annotated example per concept type.
Conformance target: OKF v0.2 (github.com/GoogleCloudPlatform/knowledge-catalog;
the exact text the org conforms to is vendored in the marketplace
repository under docs/upstream) plus the Open Science Pillars
requirements of the specification's knowledge layer
(docs/SPECIFICATION.md in open-science-pillars/marketplace).

## What a bundle is

A directory of markdown files under `knowledge/`. One concept per file;
the path is the concept's identity. `index.md` at the bundle root (and
per large subdirectory) lists every concept; `log.md` records change
history. Concepts cross-link with standard markdown links; every gotcha
links its dataset concept.

## Conformance walk (conformance, concept types, lifecycle)

Frontmatter, every concept (STRICT YAML: quote any value containing
a colon, e.g. `title: "Unmasked fill values: the sentinel list"`; the
checker red-flags unquoted ones):

- `type` (REQUIRED by OKF): `dataset`, `dataset-gotcha`, `recipe`,
  `convention`, `connector` or `finding`
- `title`, `description`, `tags` (required org-wide)
- `generated: { by: <actor>, at: <ISO datetime> }`: who wrote the
  concept and when. Actors are `human:<id>`, `process:<id>`,
  `team:<id>` or `owner/tool` (OKF v0.2 §7).
- `status`: `draft` (unreviewed; consultable but voiced as unverified),
  `stable` (ready for consumption) or `deprecated` (kept for links;
  `superseded_by` names the replacement). Trust lives outside status:
  steward approval adds `verified: { by: human:<id>, at: <ISO datetime> }`
  (independent checks append to the list), and consumers derive the
  trust tier (unverified, machine-confirmed, human-reviewed) from the
  events, keyed on the `human:` prefix.
- `stale_after: YYYY-MM-DD`: the sweep date; a concept is stale once
  today reaches it. A product baseline change pulls the date forward.
- `sources`: a list of `{ id, resource, title }` entries; the body cites
  each by a footnote (`[^id]`) so every claim resolves to a reference.
- `okf_version: "0.2"` in the root `index.md` frontmatter, the only
  frontmatter an index may carry.

Per type:

- **dataset**: `resource` (the archive URL or ShortName), a version or
  processing baseline with its verification date, and an `## Uncertainty`
  section in the body (the product's error fields and their caveats).
  Optional `trainings:` list of ARSET or equivalent training URLs.
- **dataset-gotcha**: `severity` (high, medium, low; high means silently
  wrong results and requires a matching `eval_case` id and a second
  review), a `dataset` link to its dataset concept, and at least one
  source cited from the body.
- **recipe**: `inputs`, `expected` values AND `expected_uncertainty`
  ranges, validation provenance as cited sources.
- **convention**: no required extras beyond the org-wide fields.
- **connector** and **finding**: the specification's connectors and
  findings sections state their extras; the provider bundle
  (nasa-daac-knowledge) carries live examples.

Two rules that keep bundles trustworthy:

1. **Sources or nothing.** Every gotcha and recipe claim carries a
   resolving source, cited by footnote. A source-free concept is worse
   than a gap.
2. **Facts, not instructions.** Concepts state facts about data; they never
   instruct the agent. No imperatives directed at Claude, no tool
   directives. The knowledge-linter flags instruction-like phrasing.

## Layout

```
your-repo/
├── README.md
├── CODEOWNERS              # stewards of /knowledge/
├── .github/workflows/bundle-gate.yml  # conformance and signature debt, as CI
└── knowledge/              # the bundle root
    ├── index.md            # okf_version frontmatter; every concept listed
    ├── log.md              # change history, newest first, ISO dates
    ├── datasets/           # example: datasets/example-dataset.md
    ├── gotchas/            # example: gotchas/example-gotcha.md
    ├── recipes/            # example: recipes/example-recipe.md
    └── conventions/        # example: conventions/example-convention.md
```

Copy the repository, delete the four `example-*` files once you have real
concepts, keep index.md and log.md current. Before every PR run the
conformance checker from the provider bundle repository against your
bundle root:

```
uv run <path-to-nasa-daac-knowledge>/tools/check_okf_v02.py knowledge
```

The four examples pass it with 0 errors; the warnings it reports on
them (unverified tier) are what any draft shows until a steward signs.
`.github/workflows/bundle-gate.yml` runs the same checker, the PEP 723
header check on any script, and the signature-debt measure on every
pull request and on main, and enforces zero debt on a release tag; a
repository copied from this template is gated from its first pull
request. The one edit it needs is the tag pattern, `{name}--v*`. Lint
with the knowledge-linter agent (core plugin) before every release.
