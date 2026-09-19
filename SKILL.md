---
name: amap-ev-station-collector
description: Collect public automobile charging stations within 3 km of supplied targets using AMap Web API plus the Android AMap app over ADB, preserve screenshot evidence, extract every displayed tariff period, audit omissions, and produce a grouped Excel workbook. Use for this specific AMap charging-station workflow; do not use for generic POI scraping or electric-bicycle charging research.
---

# AMap EV Station Collector

Build a verified station dataset in three separate phases: API candidate discovery, Android-app evidence capture, then offline parsing and Excel generation. Do not combine capture and interpretation into one fragile loop.

Before acting, read [references/runbook.md](references/runbook.md) completely. It defines the required 3 km scope, exclusion rules, phone state machine, evidence layout, tariff rules, checkpoint format, audit queries, and acceptance checks.

## Non-negotiable invariants

- Search only within 3 km of each input target. Keep the user's target names unchanged and preserve input order.
- Retain only identifiable, externally operating automobile charging stations. Exclude NIO stations, truck-only charging, electric-bicycle businesses, private/internal-only stations, vague unnamed POIs, and APP pages without operating information.
- Use AMap API to discover and deduplicate candidates; use the AMap Android app as the evidence source for station information and tariffs.
- Verify the station title before every capture. If the expected detail UI is absent, record the failure and return; never explore reviews, photos, parking details, advertisements, or unrelated controls.
- Capture every station, including stations without a tariff. If a tariff is displayed below the equipment section, tap the price number or price chart itself and capture the price-detail page.
- A price page need not cover 24 hours. Convert every period actually shown. Never discard a partial schedule merely because `00:00` or `23:59` is absent.
- Never infer missing periods or calculate missing electricity/service fees. Preserve displayed times and values exactly.
- Keep different equipment powers/types separate. Do not add powers or gun counts together. Do not apply one equipment type's tariff to another unless the UI explicitly associates them.
- Save progress after every station. On ADB loss or app instability, stop mutation, preserve the checkpoint, reconnect or restart AMap, and resume at the next unfinished station.
- Rebuild the final workbook by station group. Never append recovered periods as an unrelated block at the bottom of a sheet.

## Required deliverables

Produce:

1. a target-to-station list with distance for every retained candidate;
2. a deduplicated capture list keyed by AMap POI ID when available;
3. per-station screenshots, UI hierarchy/text, and metadata/checkpoint files;
4. an audit list for failures and unresolved tariff conflicts;
5. the final Excel workbook, one sheet per original target, with station rows grouped together and repeated station fields vertically merged in the presentation version.

Do not claim completion until the evidence-to-table audit in the runbook passes.
