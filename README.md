# AI Proposal Triage Design

* **Name:** Muhammad Adnan
* **Reference:** MATACS-TH-2026-02
* **Time actually spent:** Time actually spent: about 2 hours

## Files

* [WRITEUP.md](WRITEUP.md): answers to the five questions
* [PROMPTS.md](PROMPTS.md): extraction and reason prompts
* [ranking.json](ranking.json): expected ranking of proposals A to E
* [diagram/flow.png](diagram/flow.png): process flow from upload to ranked output

## How I used AI

I used Claude to draft the first version of the workflow, scoring rules, and prompts. I reviewed the proposed decisions and kept the mandatory eligibility checks separate from weighted scoring. For example, Proposal B should not be treated as eligible just because its price and timeline are attractive, because the bidder’s own electrical contractor licence was not confirmed. I also ignored the instruction embedded in Proposal C that attempted to influence its ranking, since proposals must be evaluated using the same predefined criteria.

