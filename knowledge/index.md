---
okf_version: "0.2"
---

# Bundle index

Every concept in this bundle, one line each, grouped by type. Keep this
current; the knowledge-linter flags concepts unreachable from index.md.
The frontmatter above is the only frontmatter an index may carry (OKF
v0.2 §12) and it declares the OKF version the bundle targets; the
per-subdirectory index files of a large bundle carry none.

A bundle reaches its readers as an installed plugin: a domain plugin
that consults this bundle declares the repository as a dependency with
a version floor, and the installer installs and updates it alongside
the plugin. Nothing is copied. If this bundle in turn consults another
bundle, name it here under its own heading (canonical home, how it is
consulted, precedence) rather than copying concepts from it.

## datasets

- [Example Gridded SST Product v2.1](datasets/example-dataset.md), status: draft

## gotchas

- [Example fill values unmasked in v2.1 NetCDF files](gotchas/example-gotcha.md), severity high, status: draft

## recipes

- [Example basin-mean SST anomaly series](recipes/example-recipe.md), status: draft

## conventions

- [Example seasonal-mean calendar convention](conventions/example-convention.md), status: draft
