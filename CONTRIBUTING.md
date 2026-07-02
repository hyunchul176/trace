# Contributing to TRACE

Thanks for helping keep TRACE accurate and comprehensive! The site is powered entirely by [`data.json`](./data.json) — a single array of opportunity objects. **No build step is needed**: `index.html` fetches `data.json` at runtime.

## How to add or edit an entry

1. Fork the repo and edit `data.json`.
2. Add (or update) one object using the schema below.
3. Make sure the JSON is valid (no trailing commas) and the `url` opens the **official** page.
4. Open a Pull Request describing the change and your source.

## Entry schema

```jsonc
{
  "id": "unique-kebab-case-id",            // stable, unique
  "title": "English title",
  "titleKo": "한국어 명칭",                  // optional (esp. Korean entries)
  "org": "Organizing body",
  "category": "award",                      // award | challenge | fellowship | dataset | workshop
  "subtype": "dissertation-award",          // free-form label
  "fields": ["autonomous-driving", "data-science-ML"],   // see vocabulary below
  "career": ["phd", "postdoc"],             // student | phd | postdoc | early-faculty | faculty | open
  "regions": ["global"],                    // global | north-america | europe | asia | korea
  "eligibilityNote": "Who can apply, key rules.",
  "membershipRequired": null,               // string or null
  "deadline": "2026-06-30",                 // ISO date, or null if none/recurring-only
  "recurrence": "annual-06",                // see below
  "prize": "$500 + plaque",                 // or null
  "url": "https://official-page",           // REQUIRED, must work
  "source": "https://where-you-verified",   // optional
  "verified": "2026-07-02",                 // date you checked
  "flag": null                              // short caveat, or null
}
```

### `fields` vocabulary
`planning`, `traffic-flow`, `logistics-freight`, `public-transit`, `road-safety`, `travel-behavior`, `ITS`, `autonomous-driving`, `prediction-forecasting`, `aviation`, `rail`, `maritime`, `electrification`, `optimization-OR`, `data-science-ML`, `policy-economics`, `human-factors`.

These fine-grained tags are grouped automatically in the UI (e.g. `traffic-flow` + `ITS` → **Traffic & ITS**), so just tag accurately — you don't pick the display group.

### `recurrence` — how status is shown
- `annual-06` → shown as **Annual · next ~Jun** once this year's date passes (use the month the deadline usually falls).
- `annual` → recurring, month unknown.
- `biennial` / `triennial` → every 2 / 3 years.
- `rolling` → year-round (datasets, always-open servers).
- `one-time` → a past `deadline` shows as **Closed (reference)**.
- `tbd` → not yet announced.

### Scope
`International` vs `Korean` is derived automatically: an entry is **Korean** if its `regions` includes `"korea"`, otherwise **International**. The **"Eligible from Korea only"** filter hides entries whose `regions` are limited to `north-america`-only (or otherwise exclude global/asia/korea/europe).

## Guidelines
- **Accuracy over quantity** — every entry needs a working official URL. If you can't verify a deadline, set `deadline: null` and an appropriate `recurrence`, and note it in `flag`.
- Prefer the canonical official page for `url`; put a secondary confirmation in `source`.
- Keep `eligibilityNote` concise and factual.

Questions? [Open an issue](https://github.com/hyunchul176/trace/issues).
