---
type: recipe
title: "Example basin-mean SST anomaly series"
description: "Annotated example of a recipe concept; a validated analysis pattern with expected values and uncertainty."
tags: [example, anomaly, time-series]
generated: { by: human:example-steward, at: 2026-07-04T00:00:00Z }
# inputs: the datasets and parameters the recipe consumes.
inputs:
  - dataset: ../datasets/example-dataset.md
  - region: example basin, lon [-80, 0], lat [0, 60]
  - baseline: 1991-2020
# expected values AND expected-uncertainty ranges are REQUIRED (SPEC §5.2).
# Skills read these; they never hardcode the numbers themselves.
expected:
  - quantity: basin-mean anomaly, 2023 annual
    range: [0.6, 1.1]
    units: K
expected_uncertainty:
  - quantity: basin-mean anomaly, annual
    spread: 0.15 K (one sigma across product versions v2.0 to v2.1)
    method: cross-version spread; block-bootstrap CI on the series
# sources: the validation provenance the expected values rest on (a
# published comparison, a tutorial you reproduced, your own committed
# validation run), cited from the body.
sources:
  - id: validation-note
    resource: https://example.org/validation-note
    title: "Validation note: the run that produced the expected ranges"
status: draft
stale_after: 2027-07-04
---

# Example basin-mean SST anomaly series

The validated pattern, stated factually: area-weighted mean over the region
(weights proportional to cell area, never unweighted), anomalies against the
stated baseline, and the uncertainty framing that accompanies the headline
number.[^validation-note] Keep the recipe minimal: one canonical analysis
per concept.

Workflow skills consult this concept and compare their results against the
`expected` and `expected_uncertainty` ranges above; golden notebooks assert
against the same ranges (SPEC §6).

[^validation-note]: The validation run whose spread and ranges the frontmatter quotes.
