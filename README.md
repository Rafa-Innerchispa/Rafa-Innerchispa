# Rafael Lopez / InnerChispa

**Building AI infrastructure that helps a real small technology company operate, build products, and protect human attention.**

I work at the intersection of physical infrastructure, software, local AI, cloud systems, and autonomous agents. My current focus is **InnerOS**, an agentic operating layer that grew out of a very practical problem: one person becoming the bottleneck across customers, development, servers, opportunities, operations, and everything that falls between them.

The goal is not to build another chatbot. The goal is to move the human from *remembering and chasing work* to the smaller set of decisions that still require human authority, judgment, relationships, creativity, or care.

## InnerOS / ARIA

**InnerOS is an autonomous operating system for a real small technology company. ARIA is the enterprise agent fleet that helps run it.**

The operating loop is:

```text
signal -> relevance -> memory -> decision -> delegation
       -> execution -> verification -> recovery -> evidence -> learning
```

Signals can come from email, repositories, infrastructure, business systems, customer operations, deadlines, cloud credits, devices, or other agents. InnerOS is designed to determine what matters in context, delegate to specialized capabilities, act through bounded tools, verify the result, preserve evidence, and involve a human only when needed.

A simple example became an important design lesson: an email explicitly stating that **$100 in AMD Developer Cloud credit would expire** was once classified as low importance because it looked like marketing. The correct system should understand the business context, register the resource, recommend the highest-value use, create one canonical action, follow it through, and close the loop.

That failure became part of the product.

## Hybrid, local-first AI infrastructure

InnerOS is intentionally not tied to one model vendor or one computer. It currently spans **two local AI nodes plus cloud services**.

### NVIDIA node

- Host: `ralphi-ia-ver-10`
- Ubuntu 24.04
- NVIDIA GeForce RTX 3060
- **12 GB VRAM**
- Ollama and local model services
- Hosts a large portion of the long-running operational stack: MongoDB, Qdrant, n8n, Home Assistant, messaging/integration services, MCP services, browser automation, observability and supporting runtimes

### AMD node

- Host: `ralfiia-amd`
- AMD Radeon AI PRO R9700
- **32 GiB class VRAM**
- ROCm
- vLLM OpenAI-compatible serving
- Used for larger local inference and coding workloads

InnerOS routes work by capability, privacy, cost and operational risk instead of assuming every task belongs in the cloud.

**Cloud when it adds value. Local when it does not.**

## ChatGPT, Gemini and a model-agnostic control plane

A meaningful part of this project has been built and operated through **ChatGPT as a human-facing engineering and operations interface**, connected to InnerOS through its MCP/tooling layer and real infrastructure controls.

That is part of the story, not something to hide because the current hackathon is hosted by Google.

For the **All Things Agentic Hackathon**, Gemini and Google Cloud provide the Google-native reasoning, agent and production infrastructure path. InnerOS is designed so that Gemini, local models, and other authorized model providers can participate behind the same governed operational layer.

The important architectural boundary is not the logo on the model. It is the separation between:

- reasoning;
- persistent state and memory;
- scoped tools;
- identity and permissions;
- deterministic business rules;
- verification and evidence;
- human approval boundaries.

## Current Google hackathon project

### InnerOS - ARIA Enterprise Agent Fleet

**All Things Agentic Hackathon / Fortified Enterprise Fleet**

The project is evolving from an earlier workforce-centered view into a broader and more accurate product:

> **An AI operating system that helps a small real-world technology company behave as if it had a much larger operational team.**

The hackathon build focuses on the new unified agentic operating layer: long-running task state, ownership and locks, local/cloud routing, recovery, persistent coordination, security/governance, cross-domain orchestration, executive intelligence, and Google Cloud execution.

Pre-existing foundations are disclosed rather than pretending everything was created during the hackathon.

## Workforce is proof, not the whole product

One of the products being built and operated through this environment is **Workforce**, a multi-tenant workforce operations platform for attendance, schedules, mobile check-ins, biometrics, incidents, reporting and deterministic pre-payroll.

The relationship is recursive but practical:

```text
InnerOS helps operate the company
        -> the company builds Workforce
        -> Workforce automates customer operations
```

That is the kind of loop I want AI to create: not more chat, but more useful time returned to people.

## Security and agentic defense

Allowing agents to perform real actions changes the engineering problem completely. InnerOS uses defense-in-depth principles such as:

- least-privilege tool and repository scopes;
- explicit approval gates for high-impact actions;
- isolated Git worktrees and repository locks;
- bounded command allowlists instead of arbitrary shell execution;
- tenant isolation and deterministic business rules;
- secret handling outside model-visible output;
- persistent audit/evidence records;
- stalled-work detection, retries and recovery;
- prompt/tool-injection defenses and Model Armor integration work for Google-hosted paths;
- observability of agent actions rather than trusting opaque success messages.

## AMD / ROCm

The AMD node is not decorative hardware. It is part of the local-first strategy.

Current work includes evaluating AMD's newly published **AMD Skills** approach so agents can reuse AMD-validated ROCm procedures instead of improvising hardware operations. Production upgrades remain deliberately conservative: useful infrastructure should not be sacrificed for novelty three days before a submission deadline.

## What I am trying to change

The technology is interesting, but the reason matters more.

I do not want AI to create another layer of work that I have to supervise constantly. I want it to absorb the repetitive coordination that consumes attention: monitoring, remembering, following up, checking status, connecting signals, recovering stalled work, and preparing the next safe action.

The target experience is:

> **InnerOS notices what matters, does what it safely can, and brings the human back only when the human is actually needed.**

## Projects and ecosystem

- **InnerOS / ARIA** - multi-agent operational infrastructure and company operating layer
- **Workforce** - workforce operations, attendance and pre-payroll automation
- **PC Doctor** - real-world infrastructure, networks, security, automation and building technology
- **InnerChispa** - AI infrastructure, agents, APIs, local compute and experimentation
- **InnerSpark** - technology, education and human-centered exploration

## Current priorities

1. Ship the All Things Agentic hackathon version of InnerOS with one undeniable end-to-end autonomous workflow.
2. Finish Workforce to commercial quality for real customers.
3. Make the executive-intelligence loop reliable enough that important signals no longer depend on one human remembering to look at them.
4. Keep local AI as the default when it is sufficient, while using Gemini/Google Cloud and other external resources where they genuinely add value.
5. Measure the actual outcome in time saved, errors avoided, work closed, and human attention returned.

---

**InnerChispa:** https://innerchispa.us  
**Current hackathon project:** https://devpost.com/software/innerops-aria-enterprise-agent-fleet
