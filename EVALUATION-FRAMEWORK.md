# Evaluation Framework

How to score candidates and make adoption decisions explainable.

---

## Scoring model

Score each candidate 0-5 on each dimension.  
Maximum score: **60 points**.

| Dimension | 0 | 5 | Weight |
|-----------|---|---|--------|
| **Relevance** | Irrelevant to Federico's work | Directly solves a daily problem | ×2 |
| **Delegation value** | Federico must do all the work | Fully automates the execution | ×2 |
| **Maturity** | Prototype/experimental | Battle-tested in production | ×1 |
| **Maintenance** | Abandoned | Actively maintained with roadmap | ×1 |
| **Integration** | Requires complex custom setup | Plugs into Federico's existing stack | ×1 |
| **Uniqueness** | Many better alternatives exist | Only viable option in its class | ×1 |
| **Complexity cost** | Very steep learning/setup curve | Works immediately | ×1 |
| **Security risk** | Unclear data handling, auth risks | Clear, safe, well-understood | ×1 |
| **License** | Incompatible or unclear | Open, permissive, or fair commercial | ×1 |
| **Ponytail score** | No encapsulation of complexity | Hides massive complexity behind a clean interface | ×2 |

**Weighted total = sum of (score × weight)**  
Maximum weighted score: **80 points**

---

## Scoring guide

### Relevance (×2)
Ask: **Does this remove friction from a problem Federico encounters regularly?**
- 0: No connection to Federico's work
- 2: Tangentially useful
- 3: Useful in specific contexts
- 4: Directly relevant, used often
- 5: Core to Federico's daily work

### Delegation value (×2)
Ask: **How much execution work does this remove from Federico?**
- 0: Federico still has to do everything
- 2: Saves some manual work
- 3: Handles most execution, Federico reviews
- 4: Near-fully automated with approval gate
- 5: Fully delegatable — Federico only provides intent

### Maturity
Ask: **Can we trust this in a real context?**
- 0: Early prototype, no users
- 2: Growing user base, occasional breaking changes
- 3: Stable enough for experimentation
- 4: Production-ready
- 5: Industry standard, trusted by many teams

### Maintenance
Ask: **Will this still work in 6 months?**
- 0: No commits in 12+ months, no response to issues
- 2: Slow but alive
- 3: Regular updates
- 4: Active team, responsive to issues
- 5: Backed by a company or large open source community

### Integration
Ask: **How hard is it to connect this to what Federico already uses?**
- 0: Requires rebuilding something we already have
- 2: Possible but requires significant custom work
- 3: Some setup required, documented
- 4: Plug-and-play with minor config
- 5: Works immediately with Federico's existing tools

### Uniqueness
Ask: **Is there a better alternative already adopted?**
- 0: We already have something better
- 2: Overlaps heavily with existing tools
- 3: Adds something new but has strong competition
- 4: Clear differentiation
- 5: Nothing else does what this does

### Complexity cost
Ask: **What does it cost Federico to start using this?**
- 0: Months of learning
- 2: Weeks
- 3: Days
- 4: Hours
- 5: Minutes — works immediately

### Security risk
Ask: **Is it safe to use in a real product context?**
- 0: Unknown data handling, requires full auth access
- 2: Some unknowns
- 3: Clear privacy policy, isolated from sensitive data
- 4: Well-understood, no unnecessary access
- 5: Open source, clear data flow, no phone-home

### License
Ask: **Can Federico use this without legal or commercial friction?**
- 0: No license, or restrictive/incompatible
- 2: Source-available or restrictive open source
- 3: GPL (some friction)
- 4: MIT/Apache — fully open
- 5: MIT/Apache with no commercial restrictions

### Ponytail score (×2)
Ask: **Does this encapsulate significant technical complexity behind a clean interface?**
- 0: Raw API or library — Federico still needs to build everything
- 2: Some abstraction but still requires heavy customization
- 3: Good abstraction, usable but with manual steps
- 4: Strong encapsulation, mostly works out of the box
- 5: One command / one prompt → complex result Federico couldn't build in hours

---

## Decision thresholds

| Weighted score | Classification |
|---------------|----------------|
| 65–80 | **ADOPT** — Adopt immediately |
| 50–64 | **LEARN** — Understand the concept, adopt if a real problem triggers it |
| 35–49 | **STUDY** — Track, revisit when maturity improves |
| 20–34 | **REFERENCE** — Keep the link, don't invest time |
| 0–19 | **IGNORE** — Remove from consideration |

These are guidelines. Override with documented reasoning.

---

## Evaluation record format

See `templates/tool-evaluation.md` for the full template.

When overriding a threshold classification, document:
1. Why the score doesn't reflect the real value
2. What specific condition triggers adoption
3. When to revisit

---

## Anti-patterns to avoid

- **Tool collecting:** high score doesn't mean we adopt everything. We adopt what we'll use.
- **Recency bias:** a new tool is not automatically better than a proven one.
- **Hype penalty:** if the tool is trending on Twitter but not in production anywhere, penalize maturity.
- **Solo-author risk:** single-maintainer projects score lower on maintenance unless they're exceptional.
