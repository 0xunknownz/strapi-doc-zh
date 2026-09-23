# Translation status

## Registration progress

Registered coverage: **208/353**.

Previous recorded count: **206/353**. This batch adds **2** new document paths. Embedded references to existing snippets are not counted again.

Historical counting baseline: `strapi/documentation@6a71f594f4023fee59d5877757874601b0e45f35`.

The denominator and previous count are inherited from the preceding status file; this batch did not re-inventory or fully audit all historical translations. Registered coverage must not be interpreted as the number of full-text translations that passed the checks below. Source revisions may differ by file.

## Latest full-text batch

Source commit: `strapi/documentation@d3cbe0c728c53920d40e3963c0a57cca0d68dbeb`.

| New translation | Source blob SHA | Paragraph pairs | Unchanged code blocks |
|---|---|---:|---:|
| `docs/cms/api/entity-service/filter.md` | `0ad9545ac04d3e9ef826d7e5ef512546f6e2d070` | 60 | 26 |
| `docs/cms/plugins/documentation.md` | `45afc1e90e1c80d9a01fd44bd4c9d691550bceb4` | 47 | 8 |

Checks completed for this batch:

- Both source files match the Git blob SHA returned by GitHub.
- All 155 extracted readable text units, including headings, tables, notices, and descriptions, have aligned translations. The documents contain 107 paragraph pairs.
- All 34 fenced code blocks are byte-identical to the upstream examples.
- Chinese/Latin spacing was checked, and the generated translation blob SHAs match the uploaded blobs.

MDX presentation wrappers were converted for GitHub Markdown. Interactive Guideflow content is linked, not embedded or independently translated. No runtime or Strapi 5 compatibility tests were performed.

The upstream Documentation plugin maintenance warning is preserved. A separately labeled translator note records the upstream inconsistency between the prose and example location of `mutateDocumentation`.

Machine-readable report: [2026-09-23-entity-service-documentation.json](translation-batches/2026-09-23-entity-service-documentation.json).

Only successfully committed files are included in the registration count. Historical full-text audit status remains unverified by this batch.
