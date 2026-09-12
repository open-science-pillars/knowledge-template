---
type: convention
# spheres (required, OSP): the Earth science spheres this claim spans, one
# or more of atmosphere, biosphere, cryosphere, geosphere, hydrosphere.
# Optional gcmd: GCMD science keywords as strings.
spheres: [hydrosphere]
title: "Example seasonal-mean calendar convention"
description: "Annotated example of a convention concept; a cross-cutting practice, no required extras beyond the org-wide fields."
tags: [example, calendar, seasons]
generated: { by: human:example-steward, at: 2026-07-04T00:00:00Z }
status: draft
stale_after: 2027-07-04
---

# Example seasonal-mean calendar convention

A convention concept records a cross-cutting practice that outlives any one
dataset. Example content: DJF seasonal means span a year boundary, so
December belongs to the following year's winter; resampling with
quarter-start-December frequency assigns it correctly, and a naive
January-February-December grouping within one calendar year is a trap.

State the practice and its rationale factually. If a specific dataset
violates or complicates the convention, that is a dataset-gotcha on that
dataset, not extra prose here.
