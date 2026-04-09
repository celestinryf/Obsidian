# Interview Prep Review -- Multi-Agent Adversarial Audit

> **Date:** 2026-04-07
> **Method:** 4 specialized agents independently reviewed the full Interviewing.md document and debated findings.
> **Agents:** LP Alignment Bar Raiser, STARRS Structure Coach, S3 Technical Depth (Senior Engineer), Story Diversity Adversary

---

## Executive Summary

**Your prep is strong for a junior. But you have 5 critical gaps that will cost you if not fixed.**

| Priority | Gap                                                                                    | Risk Level |
| -------- | -------------------------------------------------------------------------------------- | ---------- |
| 1        | Q13 (project failure) is a PLACEHOLDER -- you have no real failure story               | CRITICAL   |
| 2        | Story overlap: Q4 and Q8 both use UW workspaces; Q12 and Q26 are the same story        | CRITICAL   |
| 3        | 8 of 17 stories come from AWS Cost Optimizer -- over-concentration                     | HIGH       |
| 4        | Missing LPs: Think Big, Hire and Develop the Best, Frugality have no dedicated stories | HIGH       |
| 5        | Multiple answers are 5-7 minutes spoken -- interviewer will cut you off                | HIGH       |

---

## Where All 4 Agents Agreed

- **Q7 (Critical Feedback)** is your cleanest answer. All agents graded it A or A-.
- **Q9 (Architecture)** has the strongest S3 depth but is WAY too long (6-8 min spoken).
- **Q13 (Project Failure)** is an emergency. You cannot walk into Amazon with a placeholder.
- **Q10A and Q10B (Bug stories)** are impressively detailed but suspiciously polished for a junior -- be ready for "show me the code" follow-ups.
- **S3 references in Strengthen sections** are often forced. Cut them from non-S3 answers.

---

## Where Agents Disagreed

### Debate 1: Is the Cost Optimizer dominance a problem?

**STARRS Coach:** "11 of 18 answers reference the Cost Optimizer. That's fine -- it's your strongest material."

**Story Diversity Agent:** "RED FLAG. If the interviewer hears 'on my AWS Cost Optimizer' four times in a row, they'll think you only have one experience. Max 2 Cost Optimizer answers per 4-question interview."

**LP Agent:** "Siding with Diversity. The interviewer will explicitly ask 'do you have a different example?' after the second Cost Optimizer reference."

**Resolution:** Cap Cost Optimizer at 2 answers per interview. Force Club and UW for the other 2.

### Debate 2: Are the answers too polished for a junior?

**S3 Technical Agent:** "Q9 (architecture) and Q21 (Home Rec System) read like senior engineer answers. An interviewer will probe hard -- 'Did you actually build Two-Tower from scratch?' If you can't answer at the lowest level, this will hurt you."

**STARRS Coach:** "The polish is a strength, not a weakness. The depth IS the differentiator for a junior."

**LP Agent:** "The polish is fine IF you add moments of authentic struggle. Add one 'I was stuck for 6 hours because...' moment to your technical answers. Real debugging is messy, not three clean layers."

**Resolution:** Keep the depth but add 1-2 sentences of genuine confusion/struggle to Q9, Q10A, Q10B, and Q12. Make it feel lived, not rehearsed.

### Debate 3: Should every Strengthen section reference S3?

**LP Agent:** "Cut S3 references from Q4, Q5A, Q5B, Q6, Q7, Q8, Q15. They're forced. 'On the S3 team, where design decisions affect durability for billions of objects' after a story about a college club tech stack debate is cringe."

**STARRS Coach:** "Agree. Two deeply natural S3 references (Q9, Q10A) are worth more than ten bolted-on ones."

**S3 Technical Agent:** "Keep S3 in Q2, Q9, Q10A, Q12/Q26, Q17, Q18, Q19, Q20. Cut everywhere else."

**Resolution:** Strip forced S3 from 7 answers. Let genuine S3 depth in 8 answers speak for itself.

---

## Answer Grades (STARRS Coach)

| Q# | Topic | Grade | Top Issue |
|----|-------|-------|-----------|
| Q1 | Tell me about yourself | B- | No hook. Generic opener. One run-on paragraph. |
| Q2 | Why Amazon | A- | Too long (3-4 min). Pick one paragraph, save other for follow-up. |
| Q4 | Tight deadline | B+ | Result is qualitative ("positive feedback"), not quantified. |
| Q5A | Disagreement (Java vs Go) | B | Missing the prototype/benchmark data mentioned in your notes. Thin result. |
| Q5B | Disagreement (Chatbot) | A- | Strongest move (cost comparison presentation) is buried. Lead with it. |
| Q6 | Ambiguity (founding club) | B- | Activity reads like a summary, not a story. Needs specific execution detail. |
| Q7 | Critical feedback | A | Your cleanest answer. Minor: specify what the notification logic did. |
| Q8 | Technical struggle | B | Overlaps Q4 (both UW workspaces). "Struggle" part needs more wrong turns. |
| Q9 | Architecture decision | A | WAY too long (6-8 min). Needs 2-3 min core version. Offer depth on request. |
| Q10A | Bug (StorageClass enum) | A- | Also too long. Focus on Layer 1 + Layer 3. Mention Layer 2 briefly. |
| Q10B | Bug (16K god file) | A | Extremely long (7+ min). Collapse Steps 2-3. Consider swapping to Q8. |
| Q11 | AI application | B+ | Light on YOUR decisions. Add your weight-tuning reasoning. |
| Q12 | Learning new tech | B+ | Overlaps Q26. Pick one. |
| Q13 | Project failure | D | PLACEHOLDER. Emergency. |
| Q14 | REST API design | B | List of principles, not a story. Promote the error handling refactor. |
| Q15 | Testing catches bugs | B- | Reflect contradicts Activity (mentions "concurrent submissions" but bug was about unrecognized categories). Fix immediately. |
| Q23 | Teamwork | B+ | Overlaps Q5A (Java vs Go debate referenced again). Needs unique moment. |
| Q24 | Indexing | A- | "Dropped significantly" -- give a number. Cut the analogy (interviewer knows B-trees). |
| Q25 | Difficult bug (lifecycle) | A- | Same bug as Q10A Layer 3. Don't use both in same interview. |
| Q26 | Learning something new | B+ | Q12 with S3 track added. Too long. Pick one track to lead. |

---

## LP Coverage Gap Analysis (Bar Raiser)

### Over-indexed (appearing in 5+ answers)
- **Dive Deep** -- 6 stories. Your strongest LP. Risk: feels rehearsed.
- **Customer Obsession** -- present everywhere but often formulaic ("at S3 this matters because...")
- **Ownership** -- well-represented through club and end-to-end feature ownership.

### Under-indexed or MISSING
| LP | Stories | Gap |
|----|---------|-----|
| **Think Big** | Zero dedicated stories | CRITICAL. Founding the club IS Think Big but you frame it as "ambiguity." Reframe. |
| **Hire and Develop the Best** | Zero stories | CRITICAL. You're a club president who recruits teams. Where's the story about growing someone? |
| **Frugality** | Only parenthetical asides | HIGH. Need one story where "we had no budget so I did X instead of Y." |
| **Have Backbone (Commit side)** | Only the "disagree" half shown | MEDIUM. Where did you commit to a decision you disagreed with? LP is two-sided. |

---

## S3 Technical Depth Gaps (Senior Engineer)

### What's Correct
- `copy_object` with MetadataDirective/TaggingDirective -- correct
- `list_objects_v2` pagination -- correct
- Lifecycle rule merge strategy -- genuinely impressive for a junior
- Pricing math -- correct for us-east-1

### Critical Knowledge Gaps

| Gap | Why It Matters | Where to Add It |
|-----|---------------|-----------------|
| **`copy_object` has a 5 GB limit** | Objects > 5GB need multipart copy. Your executor will silently fail on large objects. | Add to Q9 Execute phase or Q20 walkthrough. |
| **128 KB minimum billable object size for IA/Glacier** | Transitioning a 1 KB object to GLACIER_IR INCREASES cost. Scanner doesn't filter on size. | Add `MIN_TRANSITION_SIZE = 128 * 1024` to scanner discussion. |
| **`LastModified` != last accessed** | An object read 10K times/day but written once 2 years ago looks "cold" to your scanner. | Acknowledge in Q20 limitations. Mention Storage Lens or CloudWatch as the fix. |
| **Versioned bucket behavior on delete** | Deleting in a versioned bucket creates a delete marker, doesn't free noncurrent versions. Storage can go UP. | Add to DELETE_STALE_OBJECT discussion. |
| **S3 Inventory vs ListObjectsV2** | S3 Inventory is orders of magnitude cheaper for scanning at scale ($0.0025/M objects vs API call costs). | Add to "how would you scale this" follow-up. |
| **Pricing is region-dependent** | Hardcoded $0.023 is us-east-1 only. ap-southeast-1 is $0.025. | Acknowledge as a simplification. |

### Killer Additions (would impress an S3 interviewer)

1. "I'd use S3 Inventory instead of ListObjectsV2 for production scanning."
2. "Objects under 128 KB should be excluded from IA/Glacier transitions."
3. "I'd check GetBucketVersioning before recommending deletes."
4. "For copy_object on objects > 5 GB, I'd need multipart copy."
5. "LastModified only tells me writes, not reads. For real coldness I'd integrate Storage Lens."

### Questions They'll Ask That You're Not Ready For

1. "Your scanner uses LastModified for coldness. How would you handle an object read 10K times/day but written once 2 years ago?"
2. "What happens when your executor runs copy_object on a 50 GB object?"
3. "A customer runs your tool on a versioned bucket and deletes 100K objects. Their storage cost goes UP. How?"
4. "Two instances of your tool run on the same bucket. What happens to lifecycle configuration?" (Race condition: read-merge-write is not atomic.)
5. "A bucket has 1 million 500-byte objects in STANDARD. Should your tool transition them to GLACIER_IR?" (No -- 128 KB minimum billing makes it more expensive.)

---

## Story Collision Map (Diversity Agent)

### Critical Overlaps

| Collision | Stories | Resolution |
|-----------|---------|------------|
| Q4 + Q8 both use UW workspaces | Tight deadline + Technical struggle | **Move Q8 to the 16K god file (Q10B) or a Cost Optimizer struggle.** |
| Q12 + Q26 are the same story | Learning Tauri/Rust | **Merge into one. Q26 is stronger (two learning tracks). Retire Q12.** |
| Q10A Layer 3 = Q25 | Same lifecycle inflation bug | **Pick one question for this bug. Don't use both in same interview.** |
| Q5A + Q23 reference Java vs Go | Disagreement + Teamwork | **Q23 needs its own unique moment, not a retread of Q5A.** |
| Stories 15 + 17 both about credentials | Defense-in-depth + Persistence | **Merge or sharply differentiate.** |

### Source Concentration

| Source | Count | Max Per Interview |
|--------|-------|-------------------|
| AWS Cost Optimizer | 8 | **2** |
| UW Intern | 4 | 2 |
| Club | 3 (one is PLACEHOLDER) | 1-2 |
| Startup Intern | 1 | 1 |
| Side Project | 1 | 0-1 |

---

## Negative Story Gap -- EMERGENCY

**You have ZERO genuine failure stories ready to go.**

| Story | Seems Like Failure? | Actually... |
|-------|-------------------|-------------|
| Q4 (rushed demo) | Deadline pressure | Win story -- you shipped under pressure |
| Q7 (unmaintainable code) | Got criticized | Growth story -- you fixed it and improved |
| Q9 (technical struggle) | Got stuck | Win story -- you whiteboarded and solved it |
| Q13 (scope creep) | Project went sideways | PLACEHOLDER -- doesn't exist yet |

Amazon WILL ask "tell me about a time you failed." Your answers must have:
1. A real bad outcome (not "it was hard but we made it")
2. YOUR specific wrong decision that caused it
3. What you'd do differently

### Stories to Develop as Genuine Failures

1. **Q13 (Scope Creep)** -- Fill in NOW. Need: specific client, specific features that crept in, specific timeline impact, specific consequence. Frame as "I failed to set up change control and it cost us X weeks."

2. **Q6 (Lifecycle savings inflation)** -- Reframe: "I shipped a calculation that overstated savings by 10x. A user could have made a bad financial decision. I caught it in testing, but the root cause was I didn't validate my formula against real billing data."

3. **NEW: A real failure from Startup or Club** -- Something you built that nobody used, a demo that bombed, a client you lost, a team member who left because of something you did or didn't do.

---

## Length Calibration

Answers that need a 2-3 minute "core version":

| Answer | Current Length (spoken) | Fix |
|--------|----------------------|-----|
| Q2 (Why Amazon) | 3-4 min | Pick one paragraph. Save other for follow-up. |
| Q9 (Architecture) | 6-8 min | Open with "I'll focus on Execute" + 30 sec on other phases. |
| Q10A (StorageClass bug) | 5+ min | Focus on Layer 1 + Layer 3. Mention Layer 2 briefly. |
| Q10B (God file) | 7+ min | Collapse Steps 2-3. Lead with characterization tests + OOP fix. |
| Q20 (Cost Optimizer walkthrough) | 8+ min | Have a 3-min version and a 5-min version. Practice both. |
| Q21 (Home Rec System) | 6+ min | Lead with pipeline stages. Offer depth on any stage. |
| Q26 (Learning new tech) | 5+ min | Lead with S3 track (more unique). Summarize Tauri track. |

**Practice saying:** "I can go deeper on any phase -- which interests you most?"

---

## Missing Questions to Prepare

| Question | Best Existing Story | Gap Level |
|----------|-------------------|-----------|
| "Time you went above and beyond" | Q11 (wrote tests nobody asked for) | MEDIUM |
| "Decision with incomplete info" | Q12 (chose heuristic weights without data) | MEDIUM |
| "Mentored someone" | NONE -- mine Club experience for onboarding | CRITICAL |
| "Worked with someone difficult" | NONE | HIGH |
| "Simplified something complex" | Q10B (16K lines to 2.8K) -- reframe | MEDIUM |
| "Took a calculated risk" | Q13 (chose unfamiliar Tauri/Rust) | LOW |
| "Biggest weakness" | NOT IN DOCUMENT | HIGH |
| "Time you made a wrong decision" | NONE (see failure gap) | CRITICAL |

---

## Specificity Fixes Needed

These are specific places where agents flagged vagueness:

| Answer | Vague Statement | Fix |
|--------|----------------|-----|
| Q1 | "cut issue resolution time by 45%" | Add: from what to what? "From ~4 hours to ~2.2 hours average" |
| Q4 | "Feedback was positive" | Add: specific quote or decision that resulted |
| Q5A | "[insert actual number here] faster" | STILL A PLACEHOLDER IN YOUR NOTES. Get the actual number. |
| Q6 | "20+ local nonprofits" | Add: "23 organizations, 7 responses, 3 signed clients" |
| Q6 | "first paying client" | Add: how much? Even "$500" grounds it |
| Q9 | "saves roughly $50/month" | Add: on how many GB? How many transitions executed? |
| Q15 | "concurrent submissions" in Reflect | BUG: Activity describes an unrecognized category bug, not concurrency. Fix the contradiction. |
| Q16 | "noticeably more relevant" | Add: by what metric? CTR? Engagement time? |
| Q21 | "within latency targets" | Add: "sub-100ms P50, sub-300ms P99" |
| Q24 | "dropped significantly" | Add: "from ~800ms to ~15ms per EXPLAIN ANALYZE" |

---

## Top 10 Action Items (Priority Order)

| # | Action | Urgency |
|---|--------|---------|
| 1 | **Develop Q13 (scope creep) into a REAL failure story with specific details** | Do today |
| 2 | **Deconflict Q4/Q8** -- move Q8 to god file refactor or Cost Optimizer struggle | Do today |
| 3 | **Merge Q12 and Q26** -- they're the same story told twice | Do today |
| 4 | **Fix Q15 Reflect contradiction** -- "concurrent submissions" vs "unrecognized category" | Do today |
| 5 | **Add a Hire and Develop the Best story** from Club (onboarding, coaching, tough calls) | This week |
| 6 | **Add a Think Big story** -- reframe founding the club as seeing an opportunity no one else saw | This week |
| 7 | **Create 2-3 minute "core versions"** of Q9, Q10A, Q10B, Q20, Q21, Q26 | This week |
| 8 | **Study 5 S3 killer additions** (5 GB copy limit, 128 KB min, versioning on delete, S3 Inventory, LastModified != last read) | This week |
| 9 | **Strip forced S3 references** from Q4, Q5A, Q5B, Q6, Q7, Q8, Q15 Strengthen sections | This week |
| 10 | **Fill in all specificity placeholders** (numbers, metrics, quotes) | Before interview |

---

## Worst-Case Interview Simulation

If the interviewer asks these 4 questions, you're in trouble:

| Order | Question | Best Story Used | What It Burns |
|-------|----------|-----------------|---------------|
| Q1 | "Tell me about a time you failed" | Story 9 (unmaintainable PR) -- your ONLY real failure | Entire failure bucket gone |
| Q2 | "Dive deep into a technical problem" | Story 5 (StorageClass bug) | Can't use for Ownership/other LPs |
| Q3 | "Disagreed with a teammate" | Story 4 (chatbot pushback) | Burns only Startup story + best "convince" story |
| Q4 | "Built something from scratch with no guidance" | Story 13 (Tauri from zero) | Burns Learn & Be Curious + "took a risk" |

**After these 4:** Zero failure stories remaining. Zero Startup stories. Non-Cost-Optimizer technical stories nearly exhausted.

**Fix:** Develop 2 more failure stories and 1 more Startup story.
