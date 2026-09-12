---
type: dataset-gotcha
# spheres (required, OSP): the Earth science spheres this claim spans, one
# or more of atmosphere, biosphere, cryosphere, geosphere, hydrosphere.
# Optional gcmd: GCMD science keywords as strings.
spheres: [hydrosphere]
title: "Example fill values unmasked in v2.1 NetCDF files"
description: "Annotated example of a gotcha concept; one trap per file."
tags: [example, fill-values]
generated: { by: human:example-steward, at: 2026-07-04T00:00:00Z }
# severity: high | medium | low. High means the trap produces silently
# wrong results (not an error, not a warning: wrong numbers). High severity
# REQUIRES a matching eval case id and a second steward review.
severity: high
# eval_case: required when severity is high; the eval case id that traps it.
eval_case: example-fill-values
# dataset: every gotcha links its dataset concept.
dataset: ../datasets/example-dataset.md
# sources: at least one resolving reference that actually supports the
# claim, cited from the body by its id. Acceptable: a product user guide
# section, an ATBD, the provider's known-issues page, a forum thread, or
# your own reproducing test committed somewhere citable.
sources:
  - id: known-issues
    resource: https://podaac.jpl.nasa.gov/dataset/EXAMPLE_SST_V2.1/known-issues#fill
    title: "Example SST v2.1 known issues: missing _FillValue attribute"
status: draft
stale_after: 2027-07-04
---

# Example fill values unmasked in v2.1 NetCDF files

**Mechanism:** one trap per concept, stated as fact. Example: v2.1 files
store missing pixels as -9999.0 but omit the `_FillValue` attribute, so
xarray does not mask them on open.[^known-issues]

**Wrong-result mode:** what silently goes wrong. Example: means and trends
computed over the raw variable are biased far cold; a basin average can
come out below freezing without any error raised.

**Correct approach:** the factual fix. Example: masking values equal to
-9999.0 after open (`ds.where(ds.sst != -9999.0)`) restores correct
statistics; v2.2 files carry the attribute and need no workaround.

**Verification:** how a reader can confirm (a check, a file to inspect, a
one-liner whose output differs when the trap is live).

[^known-issues]: The provider's known-issues entry for the missing attribute.
