---
name: tokens
description: Show what real sites measure for a section type
---

Report the measured design values across A1 Gallery for: $ARGUMENTS

1. Call `analyze_design_tokens`. Map the request onto `sectionType` and, only if the user
   named a kind of site, `websiteType`.
2. Report heading size, body size, the scale ratio between them, section padding and
   container width as ranges — p25 to p75, with the median. Never as an average.
3. Add the common heading typefaces and accent colours.
4. If `lowSample` is set, say the slice is too thin to generalise from, then re-run
   without `websiteType` and report that instead.

Finish with one sentence on what the numbers imply for the user's own build.
