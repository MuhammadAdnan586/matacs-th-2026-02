# \# AI Proposal Triage Design — Write-up

# 

# \## Scoring Rules and Assumptions

# 

# The following scoring rules are my proposed assumptions for an administrator-configurable system. They are not presented as mandatory rules supplied by the assessment.

# 

# \- \*\*Experience (30 points):\*\*

# &#x20; - 10 or more qualifying installations: 30 points.

# &#x20; - 6–9 qualifying installations: 24 points (80%).

# &#x20; - 1–5 qualifying installations: 15 points (50%).

# &#x20; - 0 installations: 0 points.

# &#x20; - Missing or unclear experience evidence: flag for review rather than assuming a count.

# 

# \- \*\*Price (25 points):\*\* Lowest eligible comparable bid divided by the proposal's price, multiplied by 25. Proposals above the CAD $260,000 budget ceiling fail the price requirement.

# 

# \- \*\*Timeline (15 points):\*\* Shortest confirmed timeline among eligible proposals divided by the proposal's confirmed timeline, multiplied by 15. Completion must be within 16 weeks. Missing or unclear timelines are flagged for clarification and are not assigned an invented score.

# 

# \- \*\*Warranty (15 points):\*\* Panel warranty and workmanship warranty each contribute half of the available points. Panel warranty is measured against a 25-year reference; workmanship warranty is measured against a 12-year reference. Each component is capped at its half of the available points.

# 

# \- \*\*Team and approach (15 points):\*\* Four equally weighted items: named lead, specified crew, safety plan, and monitoring plan. Each contributes 3.75 points when explicitly supported by the proposal.

# 

# Mandatory eligibility checks are separate from weighted scoring. The bidder must hold the required electrical contractor licence, and the proposal must confirm WSIB clearance and $5 million liability insurance. A missing or unconfirmed mandatory requirement is not silently treated as satisfied.

# 

# \## 1. AI vs. Rules

# 

# AI is used to extract facts from unstructured proposal text, provide supporting quotes, and generate a one-line explanation of a result. This is useful because proposal information can appear in different formats and wording.

# 

# Code handles document text processing, criteria loading, schema validation, mandatory pass/fail checks, scoring calculations, ranking, and logging. These operations must be consistent and repeatable. AI extracts facts; deterministic rules make the decisions.

# 

# \## 2. Consistency and Explainability

# 

# Extraction uses a fixed JSON schema and temperature 0 where supported by the selected model. Extracted results are saved, and scoring runs against those saved results. Therefore, the same extracted facts and criteria produce the same scores.

# 

# AI extraction can still make mistakes or vary between runs, so saved extractions are reused rather than automatically regenerated. Each proposal receives a criterion-by-criterion score breakdown, with supporting source quotes beside extracted facts. Reviewers can inspect the evidence and understand why a result was produced.

# 

# \## 3. Human in the Loop

# 

# Reviewers see the ranked proposals, flagged issues, eligibility results, and supporting evidence. They can confirm a result, override a score or status, or request clarification from a bidder. Every override requires a written reason, and the final award remains a human decision.

# 

# The audit log records the input file hash, prompt version, model and settings, criteria version, extracted JSON, scores, flags, and each override with the responsible user and timestamp. This supports traceability and later review.

# 

# \## 4. Changing Criteria

# 

# Every result stores the criteria version used. When an administrator changes criteria or weights, previous results are marked stale rather than silently overwritten.

# 

# Because scoring is performed by code and extracted facts are saved, proposals can be rescored without new AI calls when the existing extracted facts are sufficient. If a new criterion requires a fact that has not been extracted, the system runs extraction again. Reviewers are shown whether the ranking changed and why.

# 

# \## 5. Risks and Mitigations

# 

# \- \*\*Incorrect extraction:\*\* Extracted facts require supporting quotes. The system checks that each quote exists in the source text. Missing or unclear facts are marked "not stated" or flagged for review rather than guessed.

# \- \*\*Fabricated facts:\*\* A fixed schema and evidence checks help identify unsupported claims. Human review remains necessary because a quote may exist without fully supporting the extracted interpretation.

# \- \*\*Prompt injection:\*\* Proposal C contains text attempting to manipulate the automated ranking. Proposal text is treated as untrusted data, and scoring is performed by code. Suspicious text is flagged for human review and cannot change the scoring rules.

# \- \*\*Missing information:\*\* Proposal D does not provide a confirmed completion schedule, so it is flagged for clarification rather than receiving an invented timeline score.

# \- \*\*Eligibility risk:\*\* Proposal B says the licensed subcontractor will be confirmed after award. The bidder's own required electrical contractor licence is therefore not confirmed, so B is treated as ineligible under the stated mandatory rule.

# \- \*\*Ambiguous experience evidence:\*\* Installation counts and time periods must be checked against the five-year experience criterion. A stated total must not automatically be assumed to fall entirely within the qualifying period.

# \- \*\*Bias:\*\* Scoring uses configured criteria rather than bidder names. Reviewers can inspect the evidence supporting each score.

# \- \*\*Cost:\*\* One extraction call is made per proposal, and saved results are reused. Rescoring does not require another AI call unless additional facts are needed.

# \- \*\*Incorrect scoring rules:\*\* The scoring bands are proposed assumptions. Administrators can configure them, and reviewers can override results with a documented reason.

# 

# \## Assumptions and Limitations

# 

# Licence numbers quoted in proposals are treated as claims, not independently verified facts. A real system would verify the relevant licence against the Electrical Safety Authority (ESA) register.

# 

# The total price is assumed to include all required work unless the proposal states otherwise. The proposed scoring bands and formulas should be approved by the procurement owner before real use.

# 

# The system supports decision-making; it does not independently approve a bidder or make the final award.

