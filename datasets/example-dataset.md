---
# type is REQUIRED by OKF v0.1. For a data product it is `dataset`.
type: dataset
title: Example Gridded SST Product v2.1
description: Annotated example of a dataset concept; copy, fill, delete.
tags: [example, sst, gridded]
# timestamp: when this concept was last materially updated (ISO date).
timestamp: 2026-07-04
# resource: where the data lives; an archive URL, DOI, or provider ShortName.
resource: https://podaac.jpl.nasa.gov/dataset/EXAMPLE_SST_V2.1
# Version or processing baseline WITH the date you verified it. Baselines
# change; a version claim without a verification date goes stale invisibly.
version: v2.1 (verified 2026-07-04 against the provider catalog)
# status lifecycle (§5.6): draft → verified → stale → superseded/disputed.
# A new concept starts as draft. Steward review sets verified fields.
status: draft
# Optional: relevant ARSET or equivalent trainings.
trainings:
  - https://appliedsciences.nasa.gov/get-involved/training/english/arset-example
---

# Example Gridded SST Product v2.1

What the product is (instrument or model, level, grid, period, cadence),
how to access it (the `resource` above; note authentication needs), and how
it is structured (dimensions, coordinates, key variables with units). State
facts; do not instruct the agent (§5.8).

## Uncertainty

REQUIRED section on every dataset concept. Name the product's native
uncertainty or error fields (for example `analysis_error`), what they do
and do not capture, and the caveats a scientist must know before quoting
them. If the product has no formal error fields, say so plainly and state
what stands in for them (ensemble spread, validation statistics,
dynamical-consistency properties).

## Known issues

Link this dataset's gotcha concepts here as they accumulate:
[example-gotcha](../gotchas/example-gotcha.md).
