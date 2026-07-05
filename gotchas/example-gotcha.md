---
type: dataset-gotcha
title: Example fill values unmasked in v2.1 NetCDF files
description: Annotated example of a gotcha concept; one trap per file.
tags: [example, fill-values]
timestamp: 2026-07-04
# severity: high | medium | low. High means the trap produces silently
# wrong results (not an error, not a warning: wrong numbers). High severity
# REQUIRES a matching eval case id and a second steward review (§5.2, §5.4).
severity: high
# eval_case: required when severity is high; the eval case id that traps it.
eval_case: example-fill-values
# dataset: every gotcha links its dataset concept.
dataset: ../datasets/example-dataset.md
# evidence: at least one resolving link that actually supports the claim.
# Acceptable evidence: product user guide section, ATBD, provider known-issues
# page, forum thread, or your own reproducing test committed somewhere citable.
evidence:
  - https://podaac.jpl.nasa.gov/dataset/EXAMPLE_SST_V2.1/known-issues#fill
status: draft
---

# Example fill values unmasked in v2.1 NetCDF files

**Mechanism:** one trap per concept, stated as fact. Example: v2.1 files
store missing pixels as -9999.0 but omit the `_FillValue` attribute, so
xarray does not mask them on open.

**Wrong-result mode:** what silently goes wrong. Example: means and trends
computed over the raw variable are biased far cold; a basin average can
come out below freezing without any error raised.

**Correct approach:** the factual fix. Example: masking values equal to
-9999.0 after open (`ds.where(ds.sst != -9999.0)`) restores correct
statistics; v2.2 files carry the attribute and need no workaround.

**Verification:** how a reader can confirm (a check, a file to inspect, a
one-liner whose output differs when the trap is live).
