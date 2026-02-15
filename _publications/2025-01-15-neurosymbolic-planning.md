---
title: "NeuroSymbolic Knowledge-Grounded Planning and Reasoning in Artificial Intelligence Systems"
collection: publications
category: manuscripts
permalink: /publication/2025-ieee-neurosymbolic-planning
excerpt: "A neurosymbolic framework for knowledge-grounded, constraint-aware planning and reasoning in high-stakes AI decision support."
date: 2025-01-15
venue: "IEEE Intelligent Systems"
paperurl: "https://par.nsf.gov/servlets/purl/10632010"
citation: "Amit Sheth, Vedant Khandelwal, Kaushik Roy, Vishal Pallagani, and Megha Chakraborty. (2025). &quot;NeuroSymbolic Knowledge-Grounded Planning and Reasoning in Artificial Intelligence Systems.&quot; <i>IEEE Intelligent Systems</i>, pp. 27-34."
header:
  teaser: /images/publications/nesy_planning/figure1.png
---

<div class="paper-nesy-planning">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="nesy-graph-bg" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper presents a layered neurosymbolic approach that couples language models with symbolic reasoning and knowledge graphs to produce interpretable, constraint-aware plans.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#nesy-why">Why</a>
      <a class="paper-jump-link" href="#nesy-what">What</a>
      <a class="paper-jump-link" href="#nesy-how">How</a>
      <a class="paper-jump-link" href="#nesy-key">Key contributions</a>
    </nav>

    <section id="nesy-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Decision-support systems in domains such as health care require <strong>multistep reasoning, constraint enforcement, and regulatory compliance</strong>.</li>
        <li>LLMs generate coherent language but struggle with <strong>structured search, logical verification, and protocol adherence</strong>.</li>
        <li>Implicit knowledge representations prevent <strong>explicit state tracking, rule enforcement, and safety validation</strong>.</li>
        <li>High-stakes environments require <strong>interpretable, constraint-aware, and dynamically adaptable planning</strong>, which standalone LLMs do not guarantee.</li>
      </ul>
    </section>

    <section id="nesy-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Proposed a <strong>neurosymbolic framework</strong> integrating domain-adapted LLMs with knowledge graphs (KGs), symbolic reasoning, and constraint-aware planning.</li>
        <li>Used the LLM to generate <strong>initial candidate plans</strong> in natural language aligned to domain context.</li>
        <li>Transformed LLM outputs into <strong>structured representations</strong> compatible with KG-backed reasoning modules.</li>
        <li>Applied <strong>deductive reasoning</strong> for logical consistency and <strong>abductive reasoning</strong> to resolve incomplete or conflicting constraints.</li>
        <li>Illustrated the approach through a <strong>health-care MTSS use case</strong> involving a 16-year-old student subject to protocol and budget constraints.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/nesy_planning/figure1.png" alt="Three-layer neurosymbolic architecture integrating LLM generation with symbolic reasoning and knowledge graphs.">
        <figcaption>Figure 1. Three-layer neurosymbolic architecture integrating LLM generation with symbolic reasoning and knowledge graphs.</figcaption>
      </figure>

      <p class="paper-reference">Figure 1 shows how the LLM, symbolic modules, and knowledge graphs interact across grounding, reasoning, and planning layers.</p>
    </section>

    <section id="nesy-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li><strong>Domain-adapted LLM</strong> interprets user queries and generates candidate plans in natural language.</li>
        <li><strong>Preprocessing interface</strong> converts textual outputs into structured actions and conditions aligned with KG entities.</li>
        <li><strong>Constraint manager and safety checker</strong> validate compliance with domain rules and flag violations.</li>
        <li><strong>Symbolic inference engine</strong> applies deductive reasoning for verification and abductive reasoning for resolving gaps.</li>
        <li><strong>Temporal and resource reasoner + optimizer</strong> ensure feasibility and iteratively refine plans using past history.</li>
      </ul>
    </section>

    <section id="nesy-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduces a layered neurosymbolic architecture organized around knowledge grounding, reasoning integration, and dynamic planning.</li>
        <li>Formalizes the integration of LLM-generated plans with KG-backed constraint checking and logical verification.</li>
        <li>Demonstrates deductive and abductive reasoning over structured domain knowledge to resolve conflicts (for example, protocol versus budget).</li>
        <li>Illustrates an iterative feedback loop between LLM and symbolic modules to ensure policy-compliant, executable plans.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-nesy-planning {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-border: var(--global-border-color);
      --paper-panel: var(--global-bg-color);
      --paper-accent: var(--global-link-color);
      --paper-shadow: 0 12px 28px rgba(0, 0, 0, 0.12);
    }

    html[data-theme="dark"] .paper-nesy-planning {
      --paper-shadow: 0 16px 34px rgba(0, 0, 0, 0.33);
    }

    .paper-nesy-planning .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-nesy-planning .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.36;
    }

    .paper-nesy-planning .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-nesy-planning .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-nesy-planning .paper-jump-links {
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

    .paper-nesy-planning .paper-jump-link {
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

    .paper-nesy-planning .paper-jump-link:hover,
    .paper-nesy-planning .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-nesy-planning .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-nesy-planning .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-nesy-planning .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-nesy-planning .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-nesy-planning .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-nesy-planning .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-nesy-planning .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-nesy-planning .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-nesy-planning .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    html[data-theme="dark"] .paper-nesy-planning .paper-figure-architecture img {
      border: 1px solid rgba(255, 255, 255, 0.18);
    }

    .paper-nesy-planning .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-nesy-planning .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-nesy-planning .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-nesy-planning .paper-jump-links {
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

      .paper-nesy-planning .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-nesy-planning .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-nesy-planning .paper-section {
        padding: 1.2rem 1.1rem;
      }
    }
  </style>

  <script>
    (() => {
      const attachCitationAnchor = () => {
        const citationParagraph = Array.from(document.querySelectorAll(".page__content p")).find(
          (paragraph) => paragraph.textContent.includes("Recommended citation")
        );
        if (citationParagraph && !citationParagraph.id) {
          citationParagraph.id = "paper-citation";
        }
      };

      attachCitationAnchor();
      window.requestAnimationFrame(attachCitationAnchor);
      if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", attachCitationAnchor, { once: true });
      }
      window.addEventListener("load", attachCitationAnchor, { once: true });

      const canvas = document.getElementById("nesy-graph-bg");
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
      let modules = null;
      let edges = [];
      let packets = [];
      let ripples = [];
      let palette = null;
      let animationId = null;
      let lastFrame = 0;
      let spawnClock = 0;
      let rerouteClock = 0;

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
      const lerp = (a, b, t) => a + (b - a) * t;
      const rand = (min, max) => min + Math.random() * (max - min);

      const qPoint = (path, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * path.p0.x + 2 * inv * t * path.p1.x + t * t * path.p2.x,
          y: inv * inv * path.p0.y + 2 * inv * t * path.p1.y + t * t * path.p2.y
        };
      };

      const drawCurve = (path) => {
        ctx.moveTo(path.p0.x, path.p0.y);
        ctx.quadraticCurveTo(path.p1.x, path.p1.y, path.p2.x, path.p2.y);
      };

      const buildModules = () => {
        const x1 = width * 0.14;
        const x2 = width * 0.38;
        const x3 = width * 0.62;
        const x4 = width * 0.86;
        const yMid = height * 0.5;

        modules = {
          llm: { x: x1, y: yMid },
          grounding: { x: x2, y: yMid },
          reasoning: { x: x3, y: yMid },
          planning: { x: x4, y: yMid }
        };

        edges = [
          {
            key: "llm-grounding",
            from: modules.llm,
            to: modules.grounding,
            ctrl: { x: lerp(x1, x2, 0.52), y: yMid - 80 },
            weight: 1.9
          },
          {
            key: "grounding-reasoning",
            from: modules.grounding,
            to: modules.reasoning,
            ctrl: { x: lerp(x2, x3, 0.5), y: yMid + 70 },
            weight: 1.9
          },
          {
            key: "reasoning-planning",
            from: modules.reasoning,
            to: modules.planning,
            ctrl: { x: lerp(x3, x4, 0.5), y: yMid - 74 },
            weight: 1.9
          },
          {
            key: "planning-grounding-feedback",
            from: modules.planning,
            to: modules.grounding,
            ctrl: { x: lerp(x4, x2, 0.5), y: yMid + 124 },
            weight: 1.3,
            dashed: true
          },
          {
            key: "reasoning-llm-abductive",
            from: modules.reasoning,
            to: modules.llm,
            ctrl: { x: lerp(x3, x1, 0.48), y: yMid - 140 },
            weight: 1.2,
            dashed: true
          }
        ].map((edge) => ({
          ...edge,
          path: {
            p0: { x: edge.from.x, y: edge.from.y },
            p1: { x: edge.ctrl.x, y: edge.ctrl.y },
            p2: { x: edge.to.x, y: edge.to.y }
          }
        }));
      };

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bgColor = parseColor(styles.getPropertyValue("--global-bg-color")) || [242, 242, 242];
        const accentColor = parseColor(styles.getPropertyValue("--global-link-color")) || [60, 140, 180];
        const textColor = parseColor(styles.getPropertyValue("--global-text-color")) || [50, 56, 64];

        palette = {
          haze: mixColor(bgColor, accentColor, 0.2),
          moduleFill: mixColor(bgColor, accentColor, 0.32),
          moduleStroke: mixColor(bgColor, textColor, 0.46),
          edgeStrong: mixColor(bgColor, accentColor, 0.55),
          edgeSoft: mixColor(bgColor, textColor, 0.42),
          packetForward: mixColor(bgColor, accentColor, 0.76),
          packetBack: mixColor(bgColor, textColor, 0.68),
          pulse: mixColor(bgColor, accentColor, 0.64)
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

        buildModules();
      };

      const seedPackets = () => {
        packets = [];
        ripples = [];

        for (let i = 0; i < 16; i += 1) {
          const edge = edges[i % 3];
          packets.push({
            edge,
            t: rand(0, 1),
            speed: rand(0.08, 0.2),
            size: rand(1.6, 2.8),
            alpha: rand(0.22, 0.45),
            type: "forward"
          });
        }

        for (let i = 0; i < 7; i += 1) {
          const edge = edges[3 + (i % 2)];
          packets.push({
            edge,
            t: rand(0, 1),
            speed: rand(0.06, 0.12),
            size: rand(1.6, 2.5),
            alpha: rand(0.2, 0.38),
            type: "feedback"
          });
        }
      };

      const spawnForwardPacket = () => {
        const edge = edges[Math.floor(Math.random() * 3)];
        packets.push({
          edge,
          t: 0,
          speed: rand(0.12, 0.24),
          size: rand(1.7, 2.9),
          alpha: rand(0.24, 0.5),
          type: "forward"
        });
      };

      const spawnFeedbackPacket = () => {
        const edge = edges[3 + Math.floor(Math.random() * 2)];
        packets.push({
          edge,
          t: 0,
          speed: rand(0.06, 0.14),
          size: rand(1.6, 2.5),
          alpha: rand(0.18, 0.34),
          type: "feedback"
        });
      };

      const spawnRipple = (node) => {
        ripples.push({
          x: node.x,
          y: node.y,
          radius: 4,
          growth: rand(26, 42),
          life: 520,
          age: 0
        });
      };

      const drawBackdrop = () => {
        const glow = ctx.createRadialGradient(
          width * 0.5,
          height * 0.5,
          40,
          width * 0.5,
          height * 0.5,
          Math.max(width, height) * 0.7
        );
        glow.addColorStop(0, toRgba(palette.haze, 0.1));
        glow.addColorStop(1, "rgba(0,0,0,0)");

        ctx.fillStyle = glow;
        ctx.fillRect(0, 0, width, height);
      };

      const drawEdges = () => {
        edges.forEach((edge) => {
          if (edge.dashed) {
            ctx.setLineDash([6, 7]);
          } else {
            ctx.setLineDash([]);
          }

          ctx.strokeStyle = toRgba(edge.dashed ? palette.edgeSoft : palette.edgeStrong, edge.dashed ? 0.24 : 0.32);
          ctx.lineWidth = edge.weight;
          ctx.beginPath();
          drawCurve(edge.path);
          ctx.stroke();
        });

        ctx.setLineDash([]);
      };

      const drawModule = (node, label, accent = false) => {
        const radius = 14;
        ctx.fillStyle = toRgba(palette.moduleFill, accent ? 0.3 : 0.2);
        ctx.strokeStyle = toRgba(palette.moduleStroke, accent ? 0.45 : 0.34);
        ctx.lineWidth = 1.3;
        ctx.beginPath();
        ctx.arc(node.x, node.y, radius, 0, Math.PI * 2);
        ctx.fill();
        ctx.stroke();

        ctx.fillStyle = toRgba(palette.moduleStroke, 0.32);
        ctx.font = "600 11px ui-sans-serif, system-ui, -apple-system, Segoe UI, sans-serif";
        ctx.textAlign = "center";
        ctx.textBaseline = "top";
        ctx.fillText(label, node.x, node.y + radius + 7);
      };

      const drawModules = () => {
        drawModule(modules.llm, "LLM", true);
        drawModule(modules.grounding, "KG");
        drawModule(modules.reasoning, "Reason");
        drawModule(modules.planning, "Plan", true);
      };

      const drawPackets = () => {
        packets.forEach((packet) => {
          const point = qPoint(packet.edge.path, Math.max(0, Math.min(1, packet.t)));
          const color = packet.type === "forward" ? palette.packetForward : palette.packetBack;
          ctx.fillStyle = toRgba(color, packet.alpha);
          ctx.beginPath();
          ctx.arc(point.x, point.y, packet.size, 0, Math.PI * 2);
          ctx.fill();
        });
      };

      const drawRipples = () => {
        ripples.forEach((ripple) => {
          const lifeRatio = 1 - ripple.age / ripple.life;
          ctx.strokeStyle = toRgba(palette.pulse, lifeRatio * 0.34);
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.arc(ripple.x, ripple.y, ripple.radius, 0, Math.PI * 2);
          ctx.stroke();
        });
      };

      const updateScene = (dt) => {
        spawnClock += dt;
        rerouteClock += dt;

        if (spawnClock >= 170) {
          spawnForwardPacket();
          if (Math.random() > 0.6) {
            spawnFeedbackPacket();
          }
          spawnClock = 0;
        }

        if (rerouteClock >= 1400) {
          spawnRipple(modules.reasoning);
          if (Math.random() > 0.45) {
            spawnRipple(modules.grounding);
          }
          rerouteClock = 0;
        }

        packets = packets.filter((packet) => {
          packet.t += (packet.speed * dt) / 1000;
          return packet.t <= 1.06;
        });

        ripples = ripples.filter((ripple) => {
          ripple.age += dt;
          ripple.radius += (ripple.growth * dt) / 1000;
          return ripple.age < ripple.life;
        });
      };

      const drawFrame = () => {
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawEdges();
        drawPackets();
        drawRipples();
        drawModules();
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }

        spawnClock = 0;
        rerouteClock = 0;
        lastFrame = 0;

        updatePalette();
        resize();
        seedPackets();
        drawFrame();

        if (!prefersReducedMotion.matches) {
          const loop = (timestamp) => {
            const dt = lastFrame ? Math.min(34, timestamp - lastFrame) : 16;
            lastFrame = timestamp;
            updateScene(dt);
            drawFrame();
            animationId = window.requestAnimationFrame(loop);
          };

          animationId = window.requestAnimationFrame(loop);
        }
      };

      start();

      window.addEventListener(
        "resize",
        () => {
          resize();
          seedPackets();
          drawFrame();
        },
        { passive: true }
      );

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
        drawFrame();
      });

      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });
    })();
  </script>
</div>
