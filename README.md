\# AI Proposal Triage Design



\- \*\*Name:\*\* Muhammad Adnan

\- \*\*Reference:\*\* MATACS-TH-2026-02

\- \*\*Time actually spent:\*\* About 2 hours



\## Files



\- \[WRITEUP.md](WRITEUP.md): Answers to the five assessment questions.

\- \[PROMPTS.md](PROMPTS.md): Extraction and reasoning prompts.

\- \[ranking.json](ranking.json): Evaluation results for proposals A to E.

\- \[diagram/flow.png](diagram/flow.png): Process flow from upload to ranked output.



\## How I Used AI



I used Claude to draft the first version of the workflow, scoring rules, and prompts. I reviewed the proposed decisions and kept mandatory eligibility checks separate from weighted scoring.



For example, Proposal B should not be treated as eligible just because its price and timeline are attractive, because the bidder’s own electrical contractor licence was not confirmed. I also ignored the instruction embedded in Proposal C that attempted to influence its ranking, since proposals must be evaluated using the same predefined criteria.

