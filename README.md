Nexus Orchestrator // Adaptive Task Scheduling
https://13thrule.github.io/neuro-synchron/
Nexus Orchestrator is an experimental, high-performance task scheduling engine that moves beyond simple execution into the realm of Control Theory. It treats your software system as a living organism that must dynamically respond to environmental pressure (CPU lag) and internal trauma (task failures).
<p align="center"><img src="Neuro.png" width="800"></p>
Standard task queues use static concurrency limits. Nexus uses a Closed-Loop Feedback System to maximize throughput while guaranteeing system stability.

🧠 The Architectural Thesis

Most distributed systems fail because they are "blind." They continue to hammer dependencies or flood the event loop even when the host environment is gasping for resources.

Nexus is context-aware. It monitors the Node.js Event Loop Lag in real-time and applies a PID-inspired steering mechanism to contract or expand concurrency, ensuring the application never enters a "death spiral."

🛠️ The Engineering Pillars

1. PID-Inspired Adaptive Steering

Unlike static queues, Nexus senses the "heartbeat" of your process. If the lag exceeds a specific threshold (suggesting high GC or CPU saturation), it automatically throttles the currentConcurrency. This prevents the application from "death spiraling" under load.

2. Algorithmic Supremacy ($O(\log n)$)

By using a manual Binary Heap (Priority Queue) implementation, insertions and extractions remain logarithmic. This ensures that the orchestrator itself never becomes the source of latency, even with 10M+ tasks.

3. Circuit Breaker (Stability Pattern)

If a failure threshold is met, the system enters a "Tripped" state, halting execution to provide "breathing room" for downstream services to recover. It prioritizes the health of the entire ecosystem over the completion of a single task.

4. Mathematical Entropy (Jittered Backoff)

Nexus injects Randomized Jitter into an exponential backoff algorithm. This spreads the load across the time-domain, which is the mathematically optimal way to recover from transient failures.

🚀 Quick Start

const nexus = new NexusOrchestrator({
  initialConcurrency: 5,
  maxConcurrency: 50,
  circuitThreshold: 3,
  circuitResetTimeout: 5000,
  adaptiveSteering: true
});

// Submit tasks
nexus.submit(async () => {
  return await fetchVitalData();
}, { priority: 100 });


🌐 Deployment & GitHub Pages (The "Level 5" Guide)

If GitHub suggests a Jekyll workflow, ignore it. Jekyll is for blogs; this is a high-performance application.

Method A: The Simple Way (No Code Required)

Go to your repo Settings > Pages.

Under Build and deployment > Source, change the dropdown from "GitHub Actions" to "Deploy from a branch".

Select main and / (root), then click Save.

Your site will be live in ~60 seconds.

Method B: The "Architect" Way (Using GitHub Actions)

If you prefer using the Actions tab, use the Static HTML workflow provided in .github/workflows/deploy.yml in this repo. This bypasses Jekyll entirely and pushes your index.html directly to the edge.

Architected by CODER // 13thrule
