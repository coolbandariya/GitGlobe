# Repository data quality contract

GitGlobe combines repository metadata and derived representations for discovery. The interface should preserve the distinction between source facts and model-derived signals.

## Source and derived fields
- Repository identity and URLs should come from the source record and remain stable across pipeline stages.
- README-derived capability text is an input to semantic processing, not a verified statement of project quality.
- Embeddings, spherical coordinates, clusters, ranks, and quality estimates are derived outputs. They should be versioned or reproducible from documented pipeline inputs.
- Missing or stale source metadata should remain missing/stale; do not silently replace it with invented values.

## Invariants for pipeline changes
- Deduplicate repositories by canonical identity before publishing tiles or search results.
- Keep coordinate and tile encodings consistent between pipeline output and the renderer.
- Make model/provider failures visible in pipeline logs and avoid publishing partial output as a complete refresh.
- Preserve deterministic behavior for fixed inputs and configuration where practical.
- Keep evaluation data separate from training or tuning data to avoid misleading quality claims.

## Release checks
Run the API and pipeline test suites relevant to the change. For retrieval changes, inspect duplicate behavior and the search contract; for data refreshes, verify record counts and artifact versioning. Document changes to schemas or scoring methodology.