# Operating Principles

These are not guidelines. They are constraints.

---

## 1. Capability over tool

A tool is one implementation of a capability.  
The capability is what matters.  
Tools change. Capabilities transfer.

For every tool, ask: **what capability does this represent?**  
Document the capability. Reference the tool.

---

## 2. Execution first, understanding after

Don't require Federico to study a technology before using it.

Real problem → AI solves it → inspect the result → extract the concept → document it.

Learning happens after successful execution, not before.

---

## 3. Delegation is a first-class decision

If something can be reliably delegated: delegate it.  
If it's strategically important: learn it.  
If it requires engineering depth: understand the interface, not the implementation.  
If it's low leverage: ignore it.

Every item in this system should answer: **what does this remove from Federico?**

---

## 4. Curation over collection

Discovery is not the goal. Curation is.

```
100 discovered → 30 relevant → 15 evaluated → 8 tested → 3 adopted
```

A long list of tools is noise.  
A short list of adopted capabilities is leverage.

---

## 5. The Ponytail pattern

The most valuable resources are those that **encapsulate significant complexity behind a usable workflow**.

These are Ponytail-like: reusable capabilities that let Federico direct execution without manually implementing it.

When evaluating a tool, ask: **does this encapsulate complexity I don't want Federico to own?**

---

## 6. Every capability answers four questions

1. What problem does this help Federico solve?
2. Why does Federico need to understand this?
3. Why this instead of the alternatives?
4. What work does this remove from Federico?

If a capability cannot answer all four, it is not ready to be adopted.

---

## 7. The portfolio is a laboratory

`fedemon16i/federico-portfolio` exists as a real-world test bench.  
Use it to test Capability Packs against real problems.  
Do not use it as a dumping ground.

---

## 8. Multi-LLM compatibility

Federico uses Claude, ChatGPT, Cursor, and others.  
All capabilities should be expressed in a way that works across models.  
This system is the canonical architecture. Other systems adapt to it.

---

## 9. Git intentionality

Don't commit large downloaded repositories.  
Prefer: source URL + version + license + summary + relevant extracted files.  
Git history is a log of decisions, not a storage system.

---

## 10. Respect external systems

No scraping of private or restricted content.  
Respect robots.txt, ToS, rate limits, auth boundaries, and licenses.  
Discovery should be legal, ethical, and sustainable.

---

## 11. Optimize for Federico's time

Every hour Federico spends learning something that could be delegated is a cost.  
Every hour spent on high-leverage judgment is an investment.

The goal is:

> **Product judgment × AI leverage × execution speed.**
