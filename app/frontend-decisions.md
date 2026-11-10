# Ante dashboard: frontend decisions

Layout: wireframe variant A (review queue, player case, operators, about the score). Agreed 9 November 2026.

## Structure
1. User: national regulator's supervisory officer, sees players of all licensed operators. No operator-facing portal in the MVP.
2. Home screen: review queue, one row per player, sorted by score. Row opens the player case.
3. Screens: review queue, player case, operators, about the score (model card in the UI; text from the DS team). Per-operator model quality lives on "About the score", not on Operators.
4. Blind review hides score, band, rank, reasons and source (model list vs rule list). Enforced by the API. Needed for objective O4.
5. Review outcome: Intervention needed / No concern / Not enough data to decide, plus optional note. Stored append-only; becomes human labels.
6. Time axis: "day since first activity" (no calendar dates in the data). Replay day marked on charts.
7. Global replay slider "Data as of day N" in the header. Every dashboard GET takes `as_of_day`; the day is kept in the URL (`?day=`).
8. UI language: English.
9. Reasons are template sentences filled from SHAP values by the DS team. LLM case summary is a stretch goal only.
10. UI stack: React (Vite), own CSS on design tokens, Radix Primitives, visx. No Tailwind or component kits.
11. Desktop-first from 1280px; usable at 400px, no separate mobile design.
12. Risk bands by rank: High = top 10%, Elevated = next 10%, Low = rest; `insufficient_data` when the DS score is null.

## Visual style
13. Direction "inspector's file": cool grey-blue paper, navy ink, no casino or control-room look. Tokens in `web/src/styles/tokens.css`.
14. Risk scale is one warm family, never red/green: High = oxblood filled chip, Elevated = ochre outlined chip, Low = plain text. Band is always shown by shape and colour together.
15. Typeface: Atkinson Hyperlegible Next for everything, tabular figures in tables.
16. Light and dark themes, following the system setting.
17. The one bold element is the player timeline (risk score with band zones, deposits per day, loss-chasing days, first-high and first-rule markers, replay cut-off). Everything else stays quiet.
18. The case view leads with "Model flagged high on day X. First fixed rule fired on day Y." This is the project's core claim shown per player.

## Backend implications
19. Replay data is precomputed by the DS team for every player and day and loaded into Postgres; the slider never triggers scoring.
20. Go API calls the Python scorer over internal HTTP/JSON (gRPC only mentioned as a scaling option).
21. Dashboard behind Cloudflare Access (email one-time code); ingest uses a per-operator API key. No in-app roles in the MVP.
22. Reviews table is append-only with reviewer email from Cloudflare Access and a blind flag.
