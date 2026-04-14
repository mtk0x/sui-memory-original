# Archive Notice

This is an archived copy of the original **sui-memory** source code by [noprogllama](https://zenn.dev/noprogllama) / sakuranjunkie-staff.

- **Original repository**: `https://github.com/noprogllama/sui-memory` (no longer available)
- **Original commit**: `74381974379ea5ce26b9f83c9913b1d0bb66c947` (2026-03-24)
- **License**: MIT (as stated by the original author)

The original repository has been removed from GitHub and is not archived on Software Heritage.
This copy preserves the initial implementation as-is, with no modifications to the original source code.

The original README references noprogllama's own Zenn article as "inspiration" — this is the author referring to their own writeup, not a third party.

For the actively maintained fork with additional features and bug fixes, see [mtk0x/sui-memory](https://github.com/mtk0x/sui-memory).

## Known Issues in the Original Code

The following bugs were discovered during use and fixed in the fork:

- **FTS5 special character crash**: Search queries containing special characters (e.g. `*`, `"`, `-`) crash the FTS5 query parser (no sanitization)
- **FTS5 duplicate check bug**: Deduplication logic checks at `session_id` level instead of per-pair, causing 2nd+ pairs to be silently skipped
- **created_at type mismatch**: `strftime('%s', ...)` returns TEXT, but `created_at` is REAL — the `>=` comparison always evaluates to false, excluding all sessions from the 30-day filter
- **VM environments**: Does not work in VM/cloud environments (e.g. Claude mobile app) — hooks assume local filesystem paths
- **Context noise**: Injected memories can flood the context with low-relevance results (no quality filtering)
- **Hybrid search latency**: Vector search adds significant latency (~3s+), problematic on low-spec machines
