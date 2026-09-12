---
# type is REQUIRED by OKF. For a data product it is `dataset`.
type: dataset
# spheres (required, OSP): the Earth science spheres this claim spans, one
# or more of atmosphere, biosphere, cryosphere, geosphere, hydrosphere.
# Optional gcmd: GCMD science keywords as strings.
spheres: [hydrosphere]
title: "Example Gridded SST Product v2.1"
description: "Annotated example of a dataset concept; copy, fill, delete."
tags: [example, sst, gridded]
# generated: who wrote this concept and when (an OKF v0.2 event). The
# actor is `human:<id>`, `process:<id>`, `team:<id>` or `owner/tool`.
generated: { by: human:example-steward, at: 2026-07-04T00:00:00Z }
# resource: where the data lives; an archive URL, DOI, or provider ShortName.
resource: https://podaac.jpl.nasa.gov/dataset/EXAMPLE_SST_V2.1
# Version or processing baseline WITH the date you verified it. Baselines
# change; a version claim without a verification date goes stale invisibly.
version: "v2.1 (verified 2026-07-04 against the provider catalog)"
# status: draft (unreviewed), stable (ready to consume) or
# deprecated (kept for links; `superseded_by` names the replacement).
# A new concept starts as draft. Steward approval sets status stable AND
# adds the event that carries the trust:
#   verified: { by: human:<steward-id>, at: 2026-07-06T00:00:00Z }
# Trust is derived from events, never from status: a concept with no
# `human:` verified event is unverified whatever its status says.
status: draft
# stale_after: the sweep date; the concept is stale once today reaches
# it. A product baseline change pulls the date forward.
stale_after: 2027-07-04
# sources: every resolving reference the body cites, each with an id the
# body joins to through a footnote (`[^user-guide]`). The checker warns
# on a source no footnote cites and on a footnote no source backs.
sources:
  - id: user-guide
    resource: https://podaac.jpl.nasa.gov/dataset/EXAMPLE_SST_V2.1/docs/user-guide.pdf
    title: "Example SST v2.1 user guide: grid, variables, error fields"
# Optional: relevant ARSET or equivalent trainings.
trainings:
  - https://appliedsciences.nasa.gov/get-involved/training/english/arset-example
---

# Example Gridded SST Product v2.1

What the product is (instrument or model, level, grid, period, cadence),
how to access it (the `resource` above; note authentication needs), and how
it is structured (dimensions, coordinates, key variables with units).[^user-guide]
State facts; do not instruct the agent (knowledge is declarative).

## Uncertainty

REQUIRED section on every dataset concept. Name the product's native
uncertainty or error fields (for example `analysis_error`), what they do
and do not capture, and the caveats a scientist must know before quoting
them.[^user-guide] If the product has no formal error fields, say so
plainly and state what stands in for them (ensemble spread, validation
statistics, dynamical-consistency properties).

## Known issues

Link this dataset's gotcha concepts here as they accumulate:
[example-gotcha](../gotchas/example-gotcha.md).

[^user-guide]: The v2.1 user guide, section on the grid and the error fields.
