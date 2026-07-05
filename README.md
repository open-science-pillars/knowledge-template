# knowledge-template

A conformant, empty Open Knowledge Format (OKF) bundle to copy when starting
a new knowledge bundle, with one fully annotated example per concept type.
Conformance target: OKF v0.1 (github.com/GoogleCloudPlatform/knowledge-catalog)
plus the Open Science Pillars requirements of SPECIFICATION.md §5.

## What a bundle is

A directory of markdown files. One concept per file; the path is the
concept's identity. `index.md` at the root (and per large subdirectory)
lists every concept; `log.md` records change history. Concepts cross-link
with standard markdown links; every gotcha links its dataset concept.

## Conformance walk (SPEC §5.1, §5.2)

Frontmatter, every concept (STRICT YAML: quote any value containing
a colon, e.g. `title: "Unmasked fill values: the sentinel list"`; the
linter red-flags unquoted ones):

- `type` (REQUIRED by OKF): `dataset`, `dataset-gotcha`, `recipe`, or `convention`
- `title`, `description`, `tags`, `timestamp` (required org-wide)
- `status` (§5.6): `draft` → `verified` (with `verified` date and
  `verified_by`) → `stale` → `superseded` or `disputed`

Per type:

- **dataset**: `resource` (the archive URL or ShortName), a version or
  processing baseline with its verification date, and an `## Uncertainty`
  section in the body (the product's error fields and their caveats).
  Optional `trainings:` list of ARSET or equivalent training URLs.
- **dataset-gotcha**: `severity` (high, medium, low; high means silently
  wrong results and requires a matching eval case id and a second review),
  a link to its dataset concept, and at least one `evidence` link.
- **recipe**: inputs, expected values AND expected-uncertainty ranges,
  validation provenance as evidence links.
- **convention**: no required extras beyond the org-wide fields.

Two rules that keep bundles trustworthy:

1. **Evidence or nothing.** Every gotcha and recipe claim carries a
   resolving evidence link. An evidence-free concept is worse than a gap
   (§5.5).
2. **Facts, not instructions.** Concepts state facts about data; they never
   instruct the agent. No imperatives directed at Claude, no tool
   directives. The knowledge-linter flags instruction-like phrasing (§5.8).

## Layout

```
your-bundle/
├── index.md          # every concept listed; snapshot source metadata if pinned (§5.7)
├── log.md            # change history, newest first
├── datasets/         # example: datasets/example-dataset.md
├── gotchas/          # example: gotchas/example-gotcha.md
├── recipes/          # example: recipes/example-recipe.md
└── conventions/      # example: conventions/example-convention.md
```

Copy the bundle, delete the four `example-*` files once you have real
concepts, keep index.md and log.md current. Lint with the knowledge-linter
agent (core plugin) before every release.
