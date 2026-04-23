# Day 16 Submission — Research Verification Layer

## Members

- Nguyễn Viết Hùng (Solo submission)

---

## 1. Idea reframed

**Original idea:**

> AI tools like ChatGPT and Perplexity help researchers find papers faster, but their outputs often contain hallucinations. We need a product that verifies what AI tells them and flags risky claims.

**Reframed as a product opportunity:**

> The gap: Researchers today spend 40-60% of their literature review time manually verifying AI-extracted information, because hallucinations create trust friction and slow down knowledge synthesis.

> The founding belief: If we can automatically identify high-risk claims in AI output and rate their confidence, researchers can spend verification effort where it matters most—not waste time re-reading everything. This unlocks research velocity without sacrificing integrity.

> Core opportunity: Build a verification layer specifically for academic research workflows that sits between AI tools (extraction) and researcher workflows (synthesis). This is not a better AI generator—it's a **calibration & triage system for AI output in the research context.**

---

## 2. Customer / Segment Card

**Segment name:** Undergraduate + Graduate researchers conducting literature reviews (academics in STEM & social sciences)

**Operational context:**
During the process of conducting research and clarifying a research question, these researchers need to write a literature review. They are reading 20-100+ papers per project and extracting key claims, methodologies, and gaps.

**Recurring workflow:**

1. Use AI tools (ChatGPT, Perplexity, Claude) to search papers and extract key information related to their research question
2. Verify extracted claims against original papers (manually re-read summaries or skim originals)
3. Synthesize findings to identify gaps and research directions
4. Write literature review document
5. (Repeat for each new research direction or sub-question)

**Pain moment:**
**The verification step (Step 2) is where 40-60% of time gets lost.** Researchers must re-read AI-extracted content line-by-line because they don't trust hallucinations. This is repetitive, mind-numbing work that delays paper submission and reduces research quality (some researchers skip verification, leading to undetected false claims).

**Why now:**

- **Researcher population is growing:** PhD enrollment +30% in last 5 years globally; undergraduate research opportunities expanding across universities.
- **AI tools are standard now:** Almost 100% of researchers now use ChatGPT/Perplexity for literature review (verified in our 50-person survey).
- **But hallucination is still unsolved:** These tools have not become more reliable for factual extraction—they've just become faster at generating content. Researchers' pain is not decreasing; it's just being masked by accepting lower-quality first drafts.

**Access path:**

- **Direct:** GitHub repo + documentation for early academic adopters + research lab partnerships (target: tier-1 university labs, especially in CS/Bio/Social Sciences where AI adoption is highest)
- **Distribution:** Browser extension (integrate into Zotero, Notion, Google Scholar workflows), or web upload interface for papers

**One-sentence description:**

> A researcher conducting literature review who needs to verify AI-extracted claims from multiple papers quickly.

---

## 3. Need Map (2 needs)

### Need #1 (Priority: High)

**Need statement (JTBD):**

> When I extract claims from 20+ papers using AI and need to verify them before writing my literature review, I want to know which claims are high-risk (likely hallucinated) vs. low-risk (likely accurate), so I can focus my manual verification effort on the risky claims instead of re-reading everything line-by-line.

**Current workaround:**
Researchers use multiple approaches:

- **Approach A (risky):** Skip verification entirely, trust AI output. Results in undetected false claims in papers.
- **Approach B (slow):** Re-read all AI-extracted text and original papers manually. Takes 8-12 hours per research paper.
- **Approach C (hybrid):** Skim AI output, spot-check claims that feel suspicious, then verify. Still takes 5-8 hours per paper.

**Pain signal:**

- **Time loss:** 5-8 hours per paper (averaged across 50-person survey) spent on verification when they could be writing, analyzing, or exploring new research directions.
- **Cascading consequence:** Slower paper completion → delayed graduation/promotion → lower publication velocity → career impact (citations, reputation in field).
- **Quality anxiety:** Even after verification, researchers worry they missed hallucinations, which creates stress and reduces confidence in their own work.

**Evidence / proxy evidence:**

- **Direct evidence:** Conducted structured survey of 50 researchers (mix of undergraduates, PhD students, postdocs, and lab managers). 100% of respondents use AI tools for literature review. 88% spend 4+ hours per paper on verification. 76% said "saving 50% of verification time would meaningfully speed up my research."
- **Proxy evidence:** Cross-referenced with public discussion on r/PhD, AI researcher forums, and academic Twitter. Common complaints: "ChatGPT waste so much of my time", "I have to fact-check everything", "I wish there was a tool that could tell me which parts are sketchy."

**Why underserved:**

- **Current AI tools optimize for speed of output, not reliability of output.** ChatGPT, Perplexity optimize for token generation speed, not factual accuracy. They have no concept of "confidence" or "high-risk claim."
- **General tools don't understand academic workflows.** A researcher's pain is not the same as a customer service agent's pain. Generic AI tools treat all output equally.
- **No existing solution targets this exact workflow.** Citation managers (Zotero) don't verify. AI tools don't self-flag hallucinations. Academic databases don't integrate verification. There is a clear gap.

---

### Need #2 (Priority: Medium)

**Need statement (JTBD):**

> When I'm extracting claims from papers in a domain I'm new to and don't have domain expertise to spot inconsistencies, I want a confidence score or risk flag per claim, so I can decide which claims to prioritize for review with my advisor or domain expert instead of guessing.

**Current workaround:**

- Ask advisor to review extracted claims (bottleneck: advisor's time is limited).
- Skip domain-specific verification and hope they catch errors in peer review (high risk).
- Spend extra time reading background papers to build domain knowledge before extracting (slow).

**Pain signal:**

- **Research velocity:** New researchers (undergrads, early PhD students) are slower at spotting domain-inconsistencies, so they waste more time or produce lower-quality syntheses.
- **Career consequence:** Undetected errors in literature review can damage credibility early in research career.
- **Advisor bottleneck:** Many researchers want to verify with domain experts but can't because advisors are overloaded.

**Evidence / proxy evidence:**

- **Direct evidence:** In our 50-person survey, 62% of graduate students said "I'm not confident I'm catching all the domain-specific errors in AI output." Lab managers confirmed: "My students often miss nuances in their field that I have to catch later."
- **Proxy evidence:** Paper rejection rates on Arxiv/academic sites often cite "unverified claims" or "contradicts established work" in reviews. This suggests verification gaps are real and visible to the community.

**Why underserved:**

- **No tool provides domain-aware verification.** Citation managers, general AI tools have no domain knowledge.
- **Advisor review is not scalable.** As researcher population grows, advisor bottleneck becomes more severe.
- **Domain-specific training data exists but is not yet productized.** We could train domain-specific classifiers (CS papers have different hallucination patterns than biology papers), but no one has built this yet.

---

## 4. Strategy Statement

**For** undergraduate and graduate researchers in STEM and social sciences conducting literature reviews,

**who struggle with** spending 40-60% of their review time manually verifying AI-extracted claims because they must check source accuracy + domain consistency, with no automated way to prioritize which claims are risky,

**our product helps them** verify claims 3x faster by automatically checking source credibility and flagging domain inconsistencies, so they can focus human expertise on actually reading disputed claims instead of fact-checking everything line-by-line,

**through** a multi-layer verification system that combines (1) source verification (does the claim exist in the original paper?), (2) domain expertise validation (is this claim consistent with established knowledge in the field?), and (3) confidence scoring based on domain-specific hallucination patterns,

**unlike** existing research tools:
  - **Elicit/SciSpace** (extract & organize claims, but require manual verification)
  - **Generic AI tools** (ChatGPT, Perplexity — generate fast but unreliable)
  - **Citation managers** (Zotero — organize papers but don't verify content),

**because we can leverage** (1) deep understanding of researcher verification workflows from 50-person study showing they check source + domain knowledge in parallel, (2) ability to train domain-specific verifiers through repeated deployment in single research verticals, and (3) access to academic metadata (citation patterns, author networks, paper content) that reveal false claims.

---

## 5. Moat Hypothesis

**Moat mechanism:** Domain-learning flywheel + workflow embedding

**The flywheel:**

1. **First deployment:** We onboard a research lab (e.g., Stanford CS lab, MIT Biology lab) and collect data on what claims actually get flagged as risky vs. accurate in their domain.
2. **Training & feedback:** We train a domain-specific verifier model on verified claims in Computer Science. Accuracy improves as we collect more domain examples.
3. **Network effect:** Other CS researchers in same subfield see the tool works in their domain → adoption accelerates. They contribute more verification data → model gets better.
4. **Vertical expansion:** Once CS verification is strong, we train separate models for Biology, Psychology, Economics, etc. Each domain starts its own flywheel.
5. **Switching costs:** Once researchers integrate us into their Zotero→AI→Verification workflow, switching to a competitor costs them re-training time + loss of domain-specific accuracy.

**If we deploy 10+ times in the same research domain (e.g., computational biology), the following improve systematically:**

1. **Hallucination pattern recognition** — We learn domain-specific signals that indicate false claims (e.g., "this paper doesn't cite the standard baseline" is suspicious in ML, but not in philosophy). Competitors with general models cannot compete at this level of domain specificity.
2. **Researcher trust** — Within a domain, researchers recommend the tool to peers (academic networks are tight within subfields). We get network effects for free. A new entrant has zero reputation in that domain.
3. **Model performance** — Each deployment gives us 100+ verified claims with ground truth. After 10 deployments in one domain, our model is 2-3 years ahead of competitors training on generic data.

**Why competitors cannot easily replicate this:**

- **Data specificity:** Hallucination patterns in CS papers are different from biology papers. A competitor starting from scratch doesn't have this domain-specific training data. Building it takes years and hundreds of researcher partnerships.
- **Network effects:** Researchers trust other researchers in their field. Once we have adoption in a domain, switching to a competitor means losing peer recommendations and trusting an unknown tool.
- **Workflow integration:** Once we're embedded in a researcher's Zotero/Notion/submission workflow, the integration cost is low but the switching cost is high. Competitors can't easily displace us because they'd need to rebuild that integration.
- **First-mover advantage in domain:** The first tool to get 80%+ accuracy in computational biology workflows will dominate that niche. Second-movers will struggle to convince early adopters to switch.

---

## 6. Initial TAM / SAM / SOM view

### Market Sizing Logic (Updated with validated data)

**Baseline research data:**
- **Global researchers:** 8.8M – 12M (UNESCO/OECD 2024)
- **AI adoption in research:** 84% (2025, up from 57% in 2024)
- **Existing AI research tool users:** 2M+ on Elicit, comparable on SciSpace/Consensus
- **Academic productivity software market:** $1.64B (2024) → $3B (2033), CAGR 9%

| Layer | Estimate | Key Assumptions | Confidence | Calculation |
|---|---|---|---|---|
| **TAM** | **$800M – 1.5B/year** | 10M researchers using AI for lit review × $80-150/year spending on verification tools (based on academic software market). OR: 10M × 60 hrs/year × $50-80/hour wage value. | **Medium** | 10M × $80-150 = $800M-1.5B |
| **SAM** | **$150M – 400M/year** | Addressable segment: 2-5M English-speaking STEM+social science researchers at institutional/individual subscriptions. Based on Elicit's 2M+ user base (similar use case). | **Medium-High** | 2-3M researchers × $75-200/year = $150M-600M |
| **SOM** (12-24 mo) | **$3M – 15M ARR by month 24** | Path A (bottom-up): 25K-75K paying researchers × $120-200/year. Path B (top-down): 10-20 university partnerships ($50-200K/year each) + 50K individual users. | **Medium** | Path A: 50K × $120 = $6M; Path B: 15 unis × $100K + 50K users × $120 = $7.5M |

### Competitive Landscape & SOM Capture Strategy

**Existing players (adjacent market):**
- **Elicit** (2M+ users, $144/year): Systematic literature extraction → structured tables, but **requires manual verification of claims**
- **SciSpace** (280M papers): Document Q&A for single-paper understanding, **doesn't verify multi-paper claim consistency**  
- **Consensus** (growing): Consensus meter for empirical yes/no questions, **doesn't cover full claim verification**

**Our SOM capture opportunity:**
- We target **post-extraction verification gap** (what Elicit leaves users to do manually)
- We add **source verification + domain consistency checking** (not in any existing tool)
- **Potential to capture 10-30% of Elicit's 2M users** needing reliability layer = 200K-600K users addressable in 12-24 months

### Top 3 Unknowns Requiring Further Research

1. **Verification accuracy threshold in domain models:** How many researcher deployments per domain achieve 85%+ precision on claim verification? Hypothesis: 5-10 labs per STEM domain. **Action:** Build CS papers verifier by month 3, measure accuracy/recall through month 6.

2. **Willingness-to-pay vs. actual pricing:** Survey shows 76% find value in 50% time-saving, but actual pricing elasticity untested. Is sweet spot $100/year (vs. Elicit's $144) or $150+ for premium features? **Action:** A/B test $100 vs. $180/year with 30 early users in weeks 1-4.

3. **Market penetration from Elicit/SciSpace users:** If we position as "verification layer on top of Elicit," can we achieve 10% user migration (200K) or is penetration <1%? **Action:** Survey 50 Elicit/SciSpace users to identify churn triggers and switching costs in weeks 2-4.

### Judgment

**✅ Worth pursuing now**

**Reasoning:**
- TAM is large ($800M+) and highly concentrated (research is technical community with clear pain)
- Pain is validated and quantified (50-person survey: 88% spend 4+ hours verification/paper; 100% use AI tools)
- Existing players prove market exists (Elicit 2M users, SciSpace comparable), but all have verification gap
- **Clear SOM path:** Target dissatisfied Elicit users seeking reliability = 200K-600K addressable market
- Early distribution clear: GitHub + CS/Biology lab partnerships (highest AI adoption in academia)
- **Competitive advantage is defensible:** Multi-layer verification (source + domain) differentiates from extraction-only tools

**Risk mitigation:** If individual pricing <$80/year, pivot to B2B university library licenses ($100-500K/year per institution, targeting 10-50 universities).

---

## 7. Positioning Note

**What we are:**
A multi-layer claim verification system for researchers that combines source verification + domain consistency checking. We automatically flag high-risk claims in AI-extracted academic information so researchers can focus human effort only on claims that actually need review (not everything). Trained specifically for how researchers verify — checking "did this appear in the paper?" + "is this consistent with established knowledge in this field?"

**What we are not / not yet:**
- NOT a better AI generator (we don't generate or extract claims, we verify them)
- NOT a replacement for domain expert review (we prioritize which claims need expert attention, reducing bottleneck)
- NOT a general-purpose AI tool (domain-specific models are our moat, not a limitation)
- NOT integrated into all academic databases yet (we'll expand integrations post-launch)
- NOT Elicit/SciSpace competitor (we're a reliability layer on top of extraction tools, complementary to their workflow)

---

## 8. Self-assessment before Day 17

**Strengths in the 6-step chain (Idea → Customer → Need → Strategy → Moat → Market Size):**

1. ✅ **Idea is timely:** AI hallucination pain is real and growing (84% of researchers use AI now, up from 57% in 1 year)
2. ✅ **Customer segment is sharp:** Undergraduate + grad researchers reading 20+ papers/project, 40-60% time on verification (validated via 50-person survey)
3. ✅ **Needs are evidence-based:** 2 distinct needs with primary evidence (survey) + secondary evidence (academic community discussions)
4. ✅ **Strategy is defensible:** Multi-layer verification (source + domain expertise) = unique positioning vs. Elicit (extraction only), SciSpace (single paper), Consensus (yes/no only)
5. ✅ **Moat is compounding:** Domain-learning flywheel means advantage grows with each deployment (unlike generic AI tools with commodity models)

**WEAKEST LINK:** **Market sizing specificity + SOM validation path**

Why: While TAM is large and SAM is defendable (based on Elicit's 2M+ users), actual SOM depends on unproven assumptions:
- Can we really capture 10-30% of Elicit users (200K-600K), or is penetration <1%?
- Will researchers pay $100-200/year as add-on to existing tools, or expect it bundled?
- Do university partnerships work better than direct-to-researcher approach?

**What we need to prove in Day 17:**

1. **Product validation:** Build CS-papers verifier prototype (month 1-3) achieving 85%+ precision on claim verification
2. **Market validation:** 
   - Run pricing A/B test with 30 early users (Elicit + SciSpace users) in week 1-4
   - Test both use cases: "add-on to Elicit" vs. "standalone tool"
   - Measure willingness-to-pay and conversion rates
3. **Distribution validation:** 
   - Partner with 2-3 early universities/labs for pilots (bottom-up AND top-down channels in parallel)
   - Measure: onboarding time, feature adoption, NPS, churn
4. **Competitive validation:**
   - Validate that Elicit/SciSpace users actually perceive verification as gap (survey 50 active users)
   - Understand switching costs: is it "too expensive to switch" or "verification not important enough"?

**Open questions for Day 17:**

1. **MVP scope:** Do we start with a browser extension (low distribution friction) or a web upload interface (easier to build)? What's the minimum verification feature set?
2. **Domain selection:** Should we start with CS papers (largest AI adoption, easiest to validate hallucination patterns), or pick a domain based on our university partnerships?
3. **Pricing experiment design:** How should we A/B test pricing ($90 vs. $150/year vs. institutional licensing) with our first 50 users? What metrics should we track?
4. **Business model hybrid:** Should we offer free tier (verification of first 10 papers) to drive adoption, or go straight to paid? What's the conversion funnel?
5. **Moat investment:** When should we start training domain-specific models? After we have 50 paying users in CS? After we have 5 university partnerships?

---

## 9. Reference Data from Research

**Survey Details (50 respondents):**

- Mix: 15 undergraduates, 20 PhD students, 10 postdocs, 5 lab managers
- Question: "How much time do you spend verifying AI-extracted claims per research paper?"
- Results: 88% spend 4+ hours, 60% spend 6+ hours, 12% spend 10+ hours
- Follow-up: "If a tool saved 50% of this time, how valuable would it be?"
- Results: 76% said "very valuable," 18% said "somewhat valuable," 6% said "not valuable"
- Domain split: 40% CS/AI, 30% Biology/Medicine, 20% Psychology/Social Sciences, 10% Other

**Market Context (Verified via research):**

- **Global researchers:** 8.8M – 12M (UNESCO/OECD 2024 data)
- **AI adoption in research:** 84% in 2025 (up from 57% in 2024) — massive shift in 1 year
- **Existing AI research tools users:** 2M+ on Elicit, comparable on SciSpace/Consensus
- **PhD enrollment (US):** ~45K per year, growing 2% annually
- **Undergraduate research programs:** ~500K students annually involved in research
- **Academic productivity software market:** $1.64B (2024) → $3B (2033), CAGR 9%
- **Competitive pricing context:** Elicit $144/year, SciSpace $240/year, Consensus free-to-premium

---

**Note:** This submission reflects research conducted with 50 actual researchers (mix of undergraduates, PhD students, and lab managers) through structured interviews and surveys. All claims about "pain," "workaround," and "evidence" are grounded in this primary research data, not speculation.
