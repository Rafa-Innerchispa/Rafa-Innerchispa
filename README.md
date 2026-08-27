# Rafael Lopez / InnerChispa

**Building living AI infrastructure that helps a real small technology company operate, build products, recover from failure, and protect human attention.**

I work at the intersection of physical infrastructure, software, local AI, cloud systems, and autonomous agents. My current focus is **InnerOS**, an agentic operating layer that grew out of a very practical problem: one person becoming the bottleneck across customers, development, servers, opportunities, operations, and everything that falls between them.

The goal is not to build another chatbot. The goal is to move the human from *remembering, chasing, checking, and repairing work* to the smaller set of decisions that still require human authority, judgment, relationships, creativity, or care.

## InnerOS / ARIA

**InnerOS is a living AI operating system for a real small technology company. ARIA is the enterprise agent fleet that helps run it.**

The operating loop is:

```text
signal -> relevance -> memory -> decision -> delegation
       -> execution -> verification -> recovery -> evidence -> learning
```

Signals can come from email, repositories, infrastructure, business systems, customer operations, deadlines, cloud credits, devices, or other agents. InnerOS is designed to determine what matters in context, delegate to specialized capabilities, act through bounded tools, verify the result, preserve evidence, recover from failure, and involve a human only when needed.

A simple example became an important design lesson: an email explicitly stating that **$100 in AMD Developer Cloud credit would expire** was once classified as low importance because it looked like marketing. The correct system should understand the business context, register the resource, recommend the highest-value use, create one canonical action, follow it through, and close the loop.

That failure became part of the product.

## A living, self-healing system

A core idea in InnerOS is that failure is expected.

Agents stall. Services crash. Models make bad decisions. Workers collide. Retries can become loops. A timestamp can look like progress when nothing useful happened. Cloud resources can remain running and waste money. Human operators can simply forget to check.

InnerOS is being built so the infrastructure can **detect those failures and repair safely when policy allows**.

Current self-healing and recovery patterns include:

- agents supervising agents and long-running tasks;
- distinguishing heartbeats from actual progress;
- detecting stalled workers;
- bounded retries and recovery without resurrecting intentionally blocked tasks;
- service health guardians and controlled restarts;
- repository ownership and locks so agents do not overwrite each other;
- isolated Git worktrees for repairs and development;
- deduplication of repeated tasks and signals;
- evidence requirements before a task is considered complete;
- routing blocked work to a different model or compute resource when appropriate;
- explicit approval boundaries for repairs that would create risk or spend money.

This is not a claim that the system never fails. It is a stronger engineering claim:

> **InnerOS expects failure, detects it, repairs what it safely can, verifies the result, and records what happened.**

An important part of the hackathon story is that **InnerOS is actively being used to improve InnerOS itself**.

## Hybrid, local-first AI infrastructure

InnerOS is intentionally not tied to one model vendor or one computer. It currently spans **two local AI nodes plus cloud services and temporary cloud-burst capacity**.

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
- **~34 GB VRAM class**
- ROCm
- vLLM OpenAI-compatible serving
- Used for larger local inference and coding workloads

At the time of the current hackathon work, the AMD node is serving a Qwen3 Coder 30B-class quantized model through vLLM.

InnerOS routes work by capability, privacy, cost, available hardware and operational risk instead of assuming every task belongs in the cloud.

**Cloud when it adds value. Local when it does not.**

## Temporary AMD cloud burst

The same resource fabric can extend beyond the two physical servers when external capacity has real strategic value.

The current AMD/DigitalOcean provider path can inspect GPU capacity, estimate cost, require an approval token, enforce a short apply window, cap spend per session, and require destruction of the resource to stop billing.

A current candidate is an **AMD Instinct MI325X with 256 GB VRAM**. The intended pattern is:

```text
credit detected
  -> high-value workload identified
  -> owner approval
  -> ephemeral AMD GPU provisioned
  -> development/inference work executed
  -> tests and evidence collected
  -> resource destroyed
  -> cost recorded
```

The important point is not renting a large GPU. It is proving that the operating system can decide **where compute should exist, what work it should receive, how much it may cost, and when it must disappear**.

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
- resource routing and cost policy;
- verification and evidence;
- human approval boundaries.

## Current Google hackathon project

### InnerOS - ARIA Enterprise Agent Fleet

**All Things Agentic Hackathon / Fortified Enterprise Fleet**

The project evolved from an earlier workforce-centered view into a broader and more accurate product:

> **A living AI operating system that helps a small real-world technology company behave as if it had a much larger operational team.**

The hackathon build focuses on the new unified agentic operating layer: long-running task state, ownership and locks, local/cloud routing, recovery, persistent coordination, security/governance, cross-domain orchestration, executive intelligence, self-healing behavior, and Google Cloud execution.

Pre-existing foundations are disclosed rather than pretending everything was created during the hackathon.

## Workforce is proof, not the whole product

One of the products being built and operated through this environment is **Workforce**, a multi-tenant workforce operations platform for attendance, schedules, mobile check-ins, biometrics, incidents, reporting and deterministic pre-payroll.

The relationship is recursive but practical:

```text
InnerOS helps operate the company
        -> the company builds Workforce
        -> Workforce automates customer operations
```

Workforce remains a real commercial priority, but in the hackathon it is evidence that the agent infrastructure is operating against real software and real business requirements rather than toy tasks.

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
- bounded cloud spending and short apply windows;
- prompt/tool-injection defenses and Model Armor integration work for Google-hosted paths;
- observability of agent actions rather than trusting opaque success messages.

Google's Agentic Defense direction is especially relevant because it maps directly to problems that appear once agents can act: prompt injection, poisoned tool output, excessive privileges, data leakage and compromised runtime behavior.

## AMD / ROCm

The AMD node is not decorative hardware. It is part of the local-first strategy.

Current work includes evaluating AMD's newly published **AMD Skills** approach so agents can reuse AMD-validated ROCm procedures instead of improvising hardware operations. Production upgrades remain deliberately conservative: useful infrastructure should not be sacrificed for novelty days before a submission deadline.

## What I am trying to change

The technology is interesting, but the reason matters more.

I do not want AI to create another layer of work that I have to supervise constantly. I want it to absorb the repetitive coordination that consumes attention: monitoring, remembering, following up, checking status, connecting signals, recovering stalled work, repairing routine failures, and preparing the next safe action.

The target experience is:

> **InnerOS notices what matters, does what it safely can, repairs what it safely can, and brings the human back only when the human is actually needed.**

## Projects and ecosystem

- **InnerOS / ARIA** - multi-agent operational infrastructure and company operating layer
- **Workforce** - workforce operations, attendance and pre-payroll automation
- **PC Doctor** - real-world infrastructure, networks, security, automation and building technology
- **InnerChispa** - AI infrastructure, agents, APIs, local compute and experimentation
- **InnerSpark** - technology, education and human-centered exploration

## Current priorities

1. Ship the All Things Agentic hackathon version of InnerOS with one undeniable end-to-end autonomous workflow.
2. Demonstrate real self-healing and controlled resource orchestration, not just agent chat.
3. Finish Workforce to commercial quality for real customers.
4. Make the executive-intelligence loop reliable enough that important signals no longer depend on one human remembering to look at them.
5. Keep local AI as the default when it is sufficient, while using Gemini/Google Cloud and temporary external AMD capacity where they genuinely add value.
6. Measure the actual outcome in time saved, errors avoided, work closed, resources governed, and human attention returned.

---

**InnerChispa:** https://innerchispa.us  
**Current hackathon project:** https://devpost.com/software/innerops-aria-enterprise-agent-fleet
