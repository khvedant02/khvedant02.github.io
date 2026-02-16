---
title: "Language Models Coupled with Metacognition Can Outperform Reasoning Models"
collection: publications
category: preprints
permalink: /publication/2025-arxiv-metacognition
excerpt: 'Demonstrating that language models enhanced with metacognitive capabilities can outperform traditional reasoning models.'
date: 2025-08-01
venue: 'arXiv preprint arXiv:2508.17959'
paperurl: 'https://arxiv.org/abs/2508.17959'
tutorialurl: 'https://sofai-lm-aaailab.github.io/'
codeurl: 'https://github.com/SOFAI-LM-AAAILab/SOFAI-LM'
citation: 'Vedant Khandelwal, Francesca Rossi, Keerthiram Murugesan, Erik Miehling, Murray Campbell, Karthikeyan Natesan Ramamurthy, and Lior Horesh. (2025). &quot;Language Models Coupled with Metacognition Can Outperform Reasoning Models.&quot; <i>arXiv preprint arXiv:2508.17959</i>.'
header:
  teaser: /images/publications/metacognition/figure1.png
---

<div class="paper-metacognition">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="bg-net" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper studies whether a training-free metacognitive control loop can make a fast language model reliable enough to reduce or outperform default use of slower reasoning models.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#meta-why">Why</a>
      <a class="paper-jump-link" href="#meta-what">What</a>
      <a class="paper-jump-link" href="#meta-how">How</a>
      <a class="paper-jump-link" href="#meta-key">Key contributions</a>
      {% if page.paperurl %}
      <a class="paper-jump-link" href="{{ page.paperurl }}" target="_blank" rel="noopener noreferrer">Paper PDF</a>
      {% endif %}
    </nav>

    <section id="meta-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>LLMs are fast, but they often fail on tasks requiring strict global constraints (such as valid graph colorings) or precise localized edits (such as program repair).</li>
        <li>LRMs can be more deliberate, but they are typically slower and more compute-heavy, making default use expensive.</li>
        <li>This paper asks whether a training-free metacognitive loop can make an LLM reliable enough to reduce (or outperform) LRM usage.</li>
      </ul>
    </section>

    <section id="meta-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>We introduce SOFAI-LM, a generalized SOFAI architecture that coordinates a fast S1 (LLM) with a slower S2 (LRM) using metacognitive governance.</li>
        <li>The controller evaluates each S1 attempt, generates targeted feedback (plus small examples), and retries for T iterations before selective fallback to S2.</li>
        <li>Evaluation spans graph coloring (including size 25) and code debugging (DebugBench).</li>
        <li>On graph coloring (size 25), SOFAI-LM reaches 42% success with lower average time than the standalone LRM.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/metacognition/figure1.png" alt="SOFAI-LM architecture showing metacognitive control over S1 iterations with selective fallback to S2.">
        <figcaption>Figure 1. SOFAI-LM's metacognitive loop evaluates S1 outputs, generates feedback, and selectively falls back to S2.</figcaption>
      </figure>

      <p class="paper-reference">Figure 1 shows how the controller iterates with S1 before deciding whether to call S2.</p>
    </section>

    <section id="meta-how" class="paper-section paper-anchor">
      <h2>How it works</h2>
      <ul class="paper-list">
        <li>S1 attempt: the LLM outputs a candidate solution in a strict format.</li>
        <li>Check: the metacognition module verifies correctness (for example, conflict violations or test outcomes).</li>
        <li>Feedback: generates Single-Line versus Multi-Line feedback and can include a small corrective example.</li>
        <li>Memory: stores minimal or extended episodic traces for the next iteration.</li>
        <li>Fallback: if S1 does not converge within T, invoke S2 with Problem-Only (PO), Best Attempt (BA), or Full History (FH).</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/metacognition/figure10.png" alt="Example feedback object comparing single-line and multi-line feedback with an adaptive corrective example.">
        <figcaption>Figure 2. Concrete example of the feedback object the controller gives S1, including an induced subproblem.</figcaption>
      </figure>

      <p class="paper-reference">Figure 2 makes the feedback mechanism tangible with a real failure case and its corrective hint.</p>
    </section>

    <section id="meta-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>A training-free metacognitive feedback loop that iteratively improves an LLM without fine-tuning.</li>
        <li>A domain-grounded study showing feedback-driven LLM iterations can match or exceed a standalone LRM on graph coloring and debugging.</li>
        <li>An ablation of feedback format and episodic memory (MLF vs SLF; MEM vs EEM) and their effect on success and time.</li>
        <li>An analysis of what to pass to S2 (PO/BA/FH) and when it helps across global-constraint versus local-fix domains.</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/metacognition/figure5.png" alt="Success rate versus time comparison between SOFAI-LM and standalone LRM across graph coloring and DebugBench.">
        <figcaption>Figure 3. SOFAI-LM shifts the success-rate/time trade-off compared to using the LRM alone across graph coloring and DebugBench.</figcaption>
      </figure>

      <p class="paper-reference">Figure 3 summarizes the main efficiency-accuracy trade-off the paper measures.</p>
    </section>
  </div>

  <style>
    .paper-metacognition {
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-border: var(--global-border-color);
      --paper-panel: var(--global-bg-color);
      --paper-accent: var(--global-link-color);
      --paper-shadow: 0 12px 28px rgba(0, 0, 0, 0.12);
      position: relative;
      padding: 0.5rem 0 0.25rem;
    }

    html[data-theme="dark"] .paper-metacognition {
      --paper-shadow: 0 16px 34px rgba(0, 0, 0, 0.33);
    }

    .paper-metacognition .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-metacognition .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.35;
    }

    .paper-metacognition .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-metacognition .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-metacognition .paper-jump-links {
      display: flex;
      flex-direction: column;
      align-items: stretch;
      gap: 0.5rem;
      position: fixed;
      right: max(0.95rem, calc((100vw - 1280px) / 2 - 1.2rem));
      top: 50%;
      transform: translateY(-50%);
      width: min(220px, calc(100vw - 1.4rem));
      padding: 0.5rem;
      border: 1px solid var(--paper-border);
      border-radius: 14px;
      background: color-mix(in srgb, var(--paper-panel) 78%, transparent);
      box-shadow: 0 8px 22px rgba(0, 0, 0, 0.16);
      backdrop-filter: blur(10px);
      z-index: 30;
    }

    .paper-metacognition .paper-jump-link {
      display: block;
      border: 1px solid var(--paper-border);
      border-radius: 999px;
      background: var(--paper-panel);
      color: var(--paper-ink);
      padding: 0.35rem 0.75rem;
      font-size: 0.88rem;
      line-height: 1.2;
      text-decoration: none;
      transition: border-color 0.2s ease, color 0.2s ease;
      white-space: nowrap;
      flex: 0 0 auto;
    }

    .paper-metacognition .paper-jump-link:hover,
    .paper-metacognition .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-metacognition .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-metacognition .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: var(--paper-panel);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-metacognition .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-metacognition .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-metacognition .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-metacognition .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-metacognition .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: var(--paper-panel);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-metacognition .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    html[data-theme="dark"] .paper-metacognition .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(255, 255, 255, 0.18);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    .paper-metacognition .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-metacognition .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-metacognition .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-metacognition .paper-jump-links {
        left: 50%;
        right: auto;
        top: auto;
        bottom: calc(8px + env(safe-area-inset-bottom));
        transform: translateX(-50%);
        flex-direction: row;
        align-items: center;
        flex-wrap: nowrap;
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
        overscroll-behavior-x: contain;
        scrollbar-width: none;
        width: calc(100vw - 0.8rem);
        border-radius: 14px;
        padding: 0.42rem;
        gap: 0.42rem;
      }

      .paper-metacognition .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-metacognition .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-metacognition .paper-section {
        padding: 1.2rem 1.1rem;
      }
    }
  </style>

  <script>
    (() => {
      const citationParagraph = Array.from(document.querySelectorAll(".page__content p")).find(
        (paragraph) => paragraph.textContent.includes("Recommended citation")
      );
      if (citationParagraph && !citationParagraph.id) {
        citationParagraph.id = "paper-citation";
      }

      const canvas = document.getElementById("bg-net");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

      let width = 0;
      let height = 0;
      let dpr = 1;
      let geometry = null;
      let palette = null;
      let animationId = null;
      let lastFrame = 0;

      let s1Pulses = [];
      let s2Pulses = [];
      let feedbackPackets = [];
      let fallbackJumps = [];
      const timers = { s1: 0, s2: 0, feedback: 0, jump: 0, jumpNext: 4800 };

      const parseColor = (value) => {
        if (!value) {
          return null;
        }
        const trimmed = value.trim();
        if (trimmed.startsWith("#")) {
          const hex = trimmed.slice(1);
          if (hex.length === 3) {
            return hex.split("").map((char) => parseInt(char + char, 16));
          }
          if (hex.length === 6) {
            return [
              parseInt(hex.slice(0, 2), 16),
              parseInt(hex.slice(2, 4), 16),
              parseInt(hex.slice(4, 6), 16)
            ];
          }
        }
        const rgbMatch = trimmed.match(/rgba?\(([^)]+)\)/);
        if (rgbMatch) {
          const parts = rgbMatch[1].split(",").map((part) => parseFloat(part.trim()));
          if (parts.length >= 3) {
            return parts.slice(0, 3);
          }
        }
        return null;
      };

      const mixColor = (base, accent, amount) =>
        base.map((channel, index) => Math.round(channel + (accent[index] - channel) * amount));

      const toRgba = (rgb, alpha) => `rgba(${rgb[0]}, ${rgb[1]}, ${rgb[2]}, ${alpha})`;
      const rand = (min, max) => min + Math.random() * (max - min);

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bgColor = parseColor(styles.getPropertyValue("--global-bg-color")) || [242, 242, 242];
        const accentColor = parseColor(styles.getPropertyValue("--global-link-color")) || [82, 173, 200];
        const textColor = parseColor(styles.getPropertyValue("--global-text-color")) || [55, 60, 68];

        palette = {
          wash: mixColor(bgColor, accentColor, 0.24),
          laneS1Soft: mixColor(bgColor, accentColor, 0.22),
          laneS1: mixColor(bgColor, accentColor, 0.4),
          laneS2Soft: mixColor(bgColor, textColor, 0.2),
          laneS2: mixColor(bgColor, textColor, 0.38),
          gate: mixColor(bgColor, accentColor, 0.52),
          gateSoft: mixColor(bgColor, accentColor, 0.32),
          feedback: mixColor(bgColor, accentColor, 0.68),
          fallback: mixColor(bgColor, textColor, 0.6),
          pulseS1: mixColor(bgColor, accentColor, 0.74),
          pulseS2: mixColor(bgColor, textColor, 0.7)
        };
      };

      const qPoint = (path, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * path.p0.x + 2 * inv * t * path.p1.x + t * t * path.p2.x,
          y: inv * inv * path.p0.y + 2 * inv * t * path.p1.y + t * t * path.p2.y
        };
      };

      const drawPath = (path) => {
        ctx.moveTo(path.p0.x, path.p0.y);
        ctx.quadraticCurveTo(path.p1.x, path.p1.y, path.p2.x, path.p2.y);
      };

      const drawArrowHead = (path, color, alpha) => {
        const tip = qPoint(path, 1);
        const prev = qPoint(path, 0.965);
        const angle = Math.atan2(tip.y - prev.y, tip.x - prev.x);
        const size = 6;
        ctx.fillStyle = toRgba(color, alpha);
        ctx.beginPath();
        ctx.moveTo(tip.x, tip.y);
        ctx.lineTo(tip.x - Math.cos(angle - Math.PI / 7) * size, tip.y - Math.sin(angle - Math.PI / 7) * size);
        ctx.lineTo(tip.x - Math.cos(angle + Math.PI / 7) * size, tip.y - Math.sin(angle + Math.PI / 7) * size);
        ctx.closePath();
        ctx.fill();
      };

      const buildGeometry = () => {
        const xS1 = width * 0.22;
        const xGate = width * 0.5;
        const xS2 = width * 0.78;
        const yTop = height * 0.08;
        const yBottom = height * 0.93;
        const yGate = height * 0.5;

        geometry = {
          xS1, xGate, xS2, yTop, yBottom, yGate,
          feedbackPath: {
            p0: { x: xGate, y: yGate - 8 },
            p1: { x: (xGate + xS1) * 0.5 - 24, y: yGate - 92 },
            p2: { x: xS1, y: yGate + 8 }
          },
          jumpToS2: {
            p0: { x: xS1, y: yGate + 14 },
            p1: { x: xGate, y: yGate - 120 },
            p2: { x: xS2, y: yGate + 14 }
          },
          jumpToS1: {
            p0: { x: xS2, y: yGate + 24 },
            p1: { x: xGate, y: yGate + 128 },
            p2: { x: xS1, y: yGate + 24 }
          }
        };
      };

      const resize = () => {
        width = window.innerWidth;
        height = window.innerHeight;
        dpr = Math.max(1, Math.min(2, window.devicePixelRatio || 1));
        canvas.width = width * dpr;
        canvas.height = height * dpr;
        canvas.style.width = `${width}px`;
        canvas.style.height = `${height}px`;
        ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
        buildGeometry();
      };

      const spawnS1 = (seed = false) => {
        s1Pulses.push({
          y: seed ? rand(geometry.yTop, geometry.yBottom) : geometry.yTop - 18,
          vy: rand(92, 140),
          r: rand(1.2, 2.1),
          phase: rand(0, Math.PI * 2),
          alpha: rand(0.24, 0.42)
        });
      };

      const spawnS2 = (seed = false) => {
        s2Pulses.push({
          y: seed ? rand(geometry.yTop, geometry.yBottom) : geometry.yTop - 22,
          vy: rand(48, 76),
          r: rand(2.2, 3.5),
          phase: rand(0, Math.PI * 2),
          alpha: rand(0.28, 0.46)
        });
      };

      const spawnFeedback = () => {
        feedbackPackets.push({
          t: 0,
          dur: rand(820, 1180),
          r: rand(1.4, 2.3),
          alpha: rand(0.24, 0.42)
        });
      };

      const spawnFallbackJump = () => {
        fallbackJumps.push({
          phase: "toS2",
          t: 0,
          dur: rand(850, 1050),
          hold: rand(260, 420),
          r: rand(2.5, 3.5),
          alpha: rand(0.3, 0.48)
        });
        spawnS2(false);
      };

      const seedScene = () => {
        s1Pulses = [];
        s2Pulses = [];
        feedbackPackets = [];
        fallbackJumps = [];
        for (let i = 0; i < 16; i += 1) spawnS1(true);
        for (let i = 0; i < 5; i += 1) spawnS2(true);
      };

      const drawNetwork = (time) => {
        const wash = ctx.createRadialGradient(
          geometry.xGate,
          geometry.yGate,
          40,
          geometry.xGate,
          geometry.yGate,
          Math.max(width, height) * 0.72
        );
        wash.addColorStop(0, toRgba(palette.wash, 0.07));
        wash.addColorStop(1, "rgba(0,0,0,0)");
        ctx.fillStyle = wash;
        ctx.fillRect(0, 0, width, height);

        ctx.lineCap = "round";

        ctx.strokeStyle = toRgba(palette.laneS1Soft, 0.24);
        ctx.lineWidth = 14;
        ctx.beginPath();
        ctx.moveTo(geometry.xS1, geometry.yTop);
        ctx.lineTo(geometry.xS1, geometry.yBottom);
        ctx.stroke();

        ctx.strokeStyle = toRgba(palette.laneS1, 0.34);
        ctx.lineWidth = 1.8;
        ctx.beginPath();
        ctx.moveTo(geometry.xS1, geometry.yTop);
        ctx.lineTo(geometry.xS1, geometry.yBottom);
        ctx.stroke();

        ctx.strokeStyle = toRgba(palette.laneS2Soft, 0.22);
        ctx.lineWidth = 14;
        ctx.beginPath();
        ctx.moveTo(geometry.xS2, geometry.yTop);
        ctx.lineTo(geometry.xS2, geometry.yBottom);
        ctx.stroke();

        ctx.strokeStyle = toRgba(palette.laneS2, 0.3);
        ctx.lineWidth = 1.8;
        ctx.beginPath();
        ctx.moveTo(geometry.xS2, geometry.yTop);
        ctx.lineTo(geometry.xS2, geometry.yBottom);
        ctx.stroke();

        ctx.setLineDash([5, 7]);
        ctx.strokeStyle = toRgba(palette.feedback, 0.28);
        ctx.lineWidth = 1.6;
        ctx.beginPath();
        drawPath(geometry.feedbackPath);
        ctx.stroke();

        ctx.strokeStyle = toRgba(palette.fallback, 0.24);
        ctx.beginPath();
        drawPath(geometry.jumpToS2);
        ctx.stroke();
        ctx.beginPath();
        drawPath(geometry.jumpToS1);
        ctx.stroke();
        ctx.setLineDash([]);

        drawArrowHead(geometry.feedbackPath, palette.feedback, 0.28);
        drawArrowHead(geometry.jumpToS2, palette.fallback, 0.24);
        drawArrowHead(geometry.jumpToS1, palette.fallback, 0.24);

        const gatePulse = 0.5 + 0.5 * Math.sin(time * 0.0025);
        ctx.fillStyle = toRgba(palette.gate, 0.36);
        ctx.beginPath();
        ctx.arc(geometry.xGate, geometry.yGate, 7, 0, Math.PI * 2);
        ctx.fill();

        ctx.strokeStyle = toRgba(palette.gateSoft, 0.18 + gatePulse * 0.12);
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.arc(geometry.xGate, geometry.yGate, 12 + gatePulse * 6, 0, Math.PI * 2);
        ctx.stroke();
      };

      const updateParticles = (dt) => {
        timers.s1 += dt;
        timers.s2 += dt;
        timers.feedback += dt;
        timers.jump += dt;

        if (timers.s1 > 130) {
          spawnS1();
          timers.s1 = 0;
        }
        if (timers.s2 > 1100) {
          spawnS2();
          timers.s2 = 0;
        }
        if (timers.feedback > 760) {
          spawnFeedback();
          timers.feedback = 0;
        }
        if (timers.jump > timers.jumpNext) {
          spawnFallbackJump();
          timers.jump = 0;
          timers.jumpNext = rand(4200, 6400);
        }

        s1Pulses = s1Pulses.filter((pulse) => {
          pulse.y += pulse.vy * dt / 1000;
          return pulse.y < geometry.yBottom + 24;
        });

        s2Pulses = s2Pulses.filter((pulse) => {
          pulse.y += pulse.vy * dt / 1000;
          return pulse.y < geometry.yBottom + 26;
        });

        feedbackPackets = feedbackPackets.filter((packet) => {
          packet.t += dt;
          return packet.t <= packet.dur;
        });

        fallbackJumps = fallbackJumps.filter((jump) => {
          jump.t += dt;
          if (jump.phase === "toS2" && jump.t >= jump.dur) {
            jump.phase = "hold";
            jump.t = 0;
            return true;
          }
          if (jump.phase === "hold" && jump.t >= jump.hold) {
            jump.phase = "toS1";
            jump.t = 0;
            return true;
          }
          if (jump.phase === "toS1" && jump.t >= jump.dur) {
            spawnS1();
            return false;
          }
          return true;
        });
      };

      const drawParticles = () => {
        s1Pulses.forEach((pulse) => {
          const x = geometry.xS1 + Math.sin(pulse.y * 0.032 + pulse.phase) * 5;
          ctx.fillStyle = toRgba(palette.pulseS1, pulse.alpha);
          ctx.beginPath();
          ctx.arc(x, pulse.y, pulse.r, 0, Math.PI * 2);
          ctx.fill();
        });

        s2Pulses.forEach((pulse) => {
          const x = geometry.xS2 + Math.sin(pulse.y * 0.026 + pulse.phase) * 4;
          ctx.fillStyle = toRgba(palette.pulseS2, pulse.alpha);
          ctx.beginPath();
          ctx.arc(x, pulse.y, pulse.r, 0, Math.PI * 2);
          ctx.fill();
        });

        feedbackPackets.forEach((packet) => {
          const progress = Math.min(1, packet.t / packet.dur);
          const point = qPoint(geometry.feedbackPath, progress);
          ctx.fillStyle = toRgba(palette.feedback, packet.alpha);
          ctx.beginPath();
          ctx.arc(point.x, point.y, packet.r, 0, Math.PI * 2);
          ctx.fill();
        });

        fallbackJumps.forEach((jump) => {
          if (jump.phase === "hold") {
            ctx.strokeStyle = toRgba(palette.fallback, jump.alpha * 0.7);
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.arc(geometry.xS2, geometry.yGate + 14, 7 + (jump.t / jump.hold) * 7, 0, Math.PI * 2);
            ctx.stroke();
            return;
          }
          const path = jump.phase === "toS2" ? geometry.jumpToS2 : geometry.jumpToS1;
          const progress = Math.min(1, jump.t / jump.dur);
          const point = qPoint(path, progress);
          ctx.fillStyle = toRgba(palette.fallback, jump.alpha);
          ctx.beginPath();
          ctx.arc(point.x, point.y, jump.r, 0, Math.PI * 2);
          ctx.fill();
        });
      };

      const drawFrame = (time, dt) => {
        ctx.clearRect(0, 0, width, height);
        drawNetwork(time);
        drawParticles();
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }

        lastFrame = 0;
        timers.s1 = 0;
        timers.s2 = 0;
        timers.feedback = 0;
        timers.jump = 0;
        timers.jumpNext = rand(4200, 6400);

        updatePalette();
        resize();
        seedScene();
        drawFrame(0, 16);

        if (!prefersReducedMotion.matches) {
          const loop = (timestamp) => {
            const dt = lastFrame ? Math.min(34, timestamp - lastFrame) : 16;
            lastFrame = timestamp;
            updateParticles(dt);
            drawFrame(timestamp, dt);
            animationId = window.requestAnimationFrame(loop);
          };
          animationId = window.requestAnimationFrame(loop);
        }
      };

      window.addEventListener("resize", () => {
        resize();
        seedScene();
        if (prefersReducedMotion.matches) {
          drawFrame(performance.now(), 16);
        }
      }, { passive: true });

      start();

      const handleMotionChange = () => {
        start();
      };

      if (prefersReducedMotion.addEventListener) {
        prefersReducedMotion.addEventListener("change", handleMotionChange);
      } else if (prefersReducedMotion.addListener) {
        prefersReducedMotion.addListener(handleMotionChange);
      }

      const observer = new MutationObserver(() => {
        updatePalette();
        drawFrame(performance.now(), 16);
      });
      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });
    })();
  </script>
</div>
