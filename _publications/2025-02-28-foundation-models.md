---
title: "Towards Learning Foundation Models for Heuristic Functions to Solve Pathfinding Problems"
collection: publications
category: workshops
permalink: /publication/2025-genplan-foundation-models
excerpt: "A reinforcement learning foundation model for pathfinding heuristics that generalizes across diverse PDDL domains."
date: 2025-02-28
venue: 'GenPlan Workshop, AAAI 2025'
paperurl: "https://aair-lab.github.io/genplan25/papers/35.pdf"
slidesurl: "https://docs.google.com/presentation/d/14FIkaabtwWMK6hQsWf96tsgmYxlTL7g-ar-80FnaFd8/edit?usp=sharing"
citation: 'Vedant Khandelwal, Amit Sheth, and Forest Agostinelli. (2025). &quot;Towards Learning Foundation Models for Heuristic Functions to Solve Pathfinding Problems.&quot; <i>GenPlan Workshop, AAAI 2025</i>.'
header:
  teaser: /images/publications/towardsfm/figure1.png
---

<div class="paper-foundation-models">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="foundation-grid" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">DeepCubeAF is a reinforcement learning foundation model that learns transferable heuristic functions for pathfinding across diverse PDDL domains without relying on optimal-label supervision.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#fm-why">Why</a>
      <a class="paper-jump-link" href="#fm-what">What</a>
      <a class="paper-jump-link" href="#fm-how">How</a>
      <a class="paper-jump-link" href="#fm-key">Key contributions</a>
      {% if page.paperurl %}
      <a class="paper-jump-link" href="{{ page.paperurl }}" target="_blank" rel="noopener noreferrer">Paper PDF</a>
      {% endif %}
    </nav>

    <section id="fm-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Existing DRL-based heuristic learners require retraining for small domain changes, leading to high compute and time costs.</li>
        <li>Supervised approaches (for example, GOOSE) require optimal solution labels, which are not always obtainable for complex pathfinding domains.</li>
        <li>Domain-independent planners (for example, Fast Downward with FF heuristic) can struggle on complex or randomized domains.</li>
        <li>There is a need for a foundation model for heuristic functions that generalizes across diverse PDDL domains without assuming supervised labels.</li>
        <li>Training on limited domains restricts generalization; broader domain diversity may improve robustness.</li>
      </ul>
    </section>

    <section id="fm-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Introduced <strong>DeepCubeAF</strong>, a reinforcement learning based foundation model for learning heuristic functions across pathfinding domains.</li>
        <li>Used <strong>PDDLFUSE</strong> to generate diverse, randomized PDDL domains for training.</li>
        <li>Applied <strong>hindsight experience replay (HER)</strong> to generate additional goal states and increase training data.</li>
        <li>Represented planning problems as <strong>STRIPS Learning Graphs (SLGs)</strong> and trained a 16-layer GNN heuristic via approximate value iteration.</li>
        <li>Trained for <strong>1 million iterations</strong> (batch size 1000) and solved problems using batch weighted A* (batch size 100, weight 0.8).</li>
        <li>Achieved higher coverage than GOOSE across all eight evaluated domains and solved <strong>60%</strong> of instances on the unseen folding domain (vs. 38% for GOOSE and Fast Downward).</li>
      </ul>
    </section>

    <section id="fm-how" class="paper-section paper-anchor">
      <h2>How it works</h2>
      <ul class="paper-list">
        <li><strong>Domain generation:</strong> PDDLFUSE fuses and randomizes PDDL domains to create diverse training environments.</li>
        <li><strong>Goal augmentation:</strong> Hindsight experience replay (HER) generates additional goals from intermediate states.</li>
        <li><strong>Graph encoding:</strong> each (state, goal, domain) tuple is represented as a STRIPS Learning Graph (SLG).</li>
        <li><strong>Heuristic learning:</strong> a 16-layer message-passing GNN is trained with approximate value iteration loss.</li>
        <li><strong>Search:</strong> batch weighted A* (batch size 100, weight 0.8) uses the learned heuristic for solving.</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/towardsfm/figure1.png" alt="DeepCubeAF training pipeline with PDDLFUSE domain generation, HER goal augmentation, SLG encoding, and GNN heuristic learning.">
        <figcaption>Figure 1. DeepCubeAF training pipeline combining PDDLFUSE, HER, graph encoding, and GNN-based heuristic learning.</figcaption>
      </figure>

      <p class="paper-reference">Figure 1 illustrates how diverse domains and goals are converted into graph inputs for heuristic learning.</p>
    </section>

    <section id="fm-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduces DeepCubeAF, a reinforcement learning based foundation model for heuristic learning in pathfinding.</li>
        <li>Proposes enhanced PDDLFUSE with adaptive negation and planner-aligned action generation to produce solvable and diverse domains.</li>
        <li>Demonstrates improved generalization over supervised GNN heuristics (GOOSE) across eight domains and leave-one-out settings.</li>
        <li>Shows competitive or superior performance to Fast Downward (FF heuristic) on several domains and improved generalization to an unseen domain.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-foundation-models {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-border: var(--global-border-color);
      --paper-panel: var(--global-bg-color);
      --paper-accent: var(--global-link-color);
      --paper-accent-soft: var(--global-link-color-hover);
      --paper-shadow: 0 12px 28px rgba(0, 0, 0, 0.12);
    }

    html[data-theme="dark"] .paper-foundation-models {
      --paper-shadow: 0 16px 34px rgba(0, 0, 0, 0.33);
    }

    .paper-foundation-models .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-foundation-models .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.38;
    }

    .paper-foundation-models .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-foundation-models .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-foundation-models .paper-jump-links {
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

    .paper-foundation-models .paper-jump-link {
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

    .paper-foundation-models .paper-jump-link:hover,
    .paper-foundation-models .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-foundation-models .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-foundation-models .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-foundation-models .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-foundation-models .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-foundation-models .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), var(--paper-accent-soft));
    }

    .paper-foundation-models .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-foundation-models .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-foundation-models .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      box-sizing: border-box;
      padding: 0.35rem;
    }

    html[data-theme="dark"] .paper-foundation-models .paper-figure img {
      border: 1px solid rgba(255, 255, 255, 0.16);
    }

    .paper-foundation-models .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-foundation-models .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-foundation-models .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-foundation-models .paper-jump-links {
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

      .paper-foundation-models .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-foundation-models .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-foundation-models .paper-section {
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

      const canvas = document.getElementById("foundation-grid");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");
      const rand = (min, max) => min + Math.random() * (max - min);
      const clamp = (value, min, max) => Math.max(min, Math.min(max, value));
      const lerp = (a, b, t) => a + (b - a) * t;

      let width = 0;
      let height = 0;
      let dpr = 1;
      let nodes = [];
      let edges = [];
      let edgeLookup = new Map();
      let pathNodeIds = [];
      let packets = [];
      let frontierTimer = 0;
      let animationId = null;
      let lastFrame = 0;
      let palette = null;
      let pulse = 0;

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

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bg = parseColor(styles.getPropertyValue("--global-bg-color")) || [242, 242, 242];
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [72, 145, 172];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [54, 58, 64];

        palette = {
          wash: mixColor(bg, accent, 0.24),
          edge: mixColor(bg, text, 0.35),
          edgePath: mixColor(bg, accent, 0.78),
          node: mixColor(bg, text, 0.58),
          nodePath: mixColor(bg, accent, 0.9),
          goal: mixColor(bg, accent, 0.95),
          packet: mixColor(bg, accent, 0.92),
          packetSoft: mixColor(bg, text, 0.68),
          ringNear: mixColor(bg, accent, 0.62),
          ringFar: mixColor(bg, text, 0.42),
          sweep: mixColor(bg, accent, 0.58)
        };
      };

      const buildGraph = () => {
        const cols = 9;
        const rows = 6;
        const xStart = width * 0.08;
        const xEnd = width * 0.92;
        const yStart = height * 0.18;
        const yEnd = height * 0.82;
        const dx = (xEnd - xStart) / (cols - 1);
        const dy = (yEnd - yStart) / (rows - 1);

        nodes = [];
        edges = [];
        edgeLookup = new Map();
        pathNodeIds = [];

        for (let c = 0; c < cols; c += 1) {
          for (let r = 0; r < rows; r += 1) {
            const jitterX = rand(-dx * 0.08, dx * 0.08);
            const jitterY = rand(-dy * 0.09, dy * 0.09);
            nodes.push({
              id: `${c}-${r}`,
              c,
              r,
              x: xStart + c * dx + jitterX,
              y: yStart + r * dy + jitterY,
              radius: rand(2.1, 3.4)
            });
          }
        }

        const nodeById = new Map(nodes.map((node) => [node.id, node]));
        const pathRows = [4, 4, 3, 3, 2, 2, 3, 3, 2];
        pathNodeIds = pathRows.map((row, col) => `${col}-${row}`);

        for (let c = 0; c < cols - 1; c += 1) {
          for (let r = 0; r < rows; r += 1) {
            const from = nodeById.get(`${c}-${r}`);
            [-1, 0, 1].forEach((delta) => {
              const rr = r + delta;
              if (rr < 0 || rr >= rows) {
                return;
              }
              const to = nodeById.get(`${c + 1}-${rr}`);
              const edge = { from, to, key: `${from.id}->${to.id}` };
              edges.push(edge);
              edgeLookup.set(edge.key, edge);
            });
          }
        }
      };

      const pointOnEdge = (edge, t) => ({
        x: lerp(edge.from.x, edge.to.x, t),
        y: lerp(edge.from.y, edge.to.y, t)
      });

      const spawnPacket = (focusPath = false) => {
        let edge = null;

        if (focusPath || Math.random() < 0.58) {
          const idx = Math.floor(rand(0, pathNodeIds.length - 1));
          const key = `${pathNodeIds[idx]}->${pathNodeIds[idx + 1]}`;
          edge = edgeLookup.get(key) || null;
        }

        if (!edge) {
          edge = edges[Math.floor(rand(0, edges.length))] || null;
        }

        if (!edge) {
          return;
        }

        packets.push({
          edge,
          t: 0,
          speed: rand(0.5, 0.95),
          radius: focusPath ? rand(2.1, 3.4) : rand(1.4, 2.5),
          alpha: focusPath ? rand(0.28, 0.44) : rand(0.16, 0.31),
          hot: focusPath || Math.random() < 0.32
        });
      };

      const drawBackdrop = () => {
        const wash = ctx.createRadialGradient(
          width * 0.62,
          height * 0.54,
          24,
          width * 0.62,
          height * 0.54,
          Math.max(width, height) * 0.76
        );
        wash.addColorStop(0, toRgba(palette.wash, 0.1));
        wash.addColorStop(1, "rgba(0, 0, 0, 0)");
        ctx.fillStyle = wash;
        ctx.fillRect(0, 0, width, height);
      };

      const drawHeuristicBands = (goalNode) => {
        const rings = [130, 220, 320, 430];
        const ringPulse = 1 + Math.sin(pulse * 1.7) * 0.035;

        rings.forEach((radius, index) => {
          const alpha = clamp(0.16 - index * 0.02, 0.05, 0.2);
          ctx.strokeStyle = toRgba(index < 2 ? palette.ringNear : palette.ringFar, alpha);
          ctx.lineWidth = index === 0 ? 1.8 : 1.2;
          ctx.setLineDash(index % 2 === 0 ? [8, 7] : [3, 7]);
          ctx.lineDashOffset = -pulse * (2 + index);
          ctx.beginPath();
          ctx.arc(goalNode.x, goalNode.y, radius * ringPulse, 0, Math.PI * 2);
          ctx.stroke();
        });
        ctx.setLineDash([]);
      };

      const drawEdges = () => {
        const pathPairs = new Set(
          pathNodeIds.slice(0, -1).map((id, index) => `${id}->${pathNodeIds[index + 1]}`)
        );

        ctx.lineCap = "round";
        edges.forEach((edge) => {
          const isPath = pathPairs.has(edge.key);
          ctx.strokeStyle = isPath ? toRgba(palette.edgePath, 0.32) : toRgba(palette.edge, 0.16);
          ctx.lineWidth = isPath ? 2 : 1;
          ctx.beginPath();
          ctx.moveTo(edge.from.x, edge.from.y);
          ctx.lineTo(edge.to.x, edge.to.y);
          ctx.stroke();
        });

        ctx.strokeStyle = toRgba(palette.edgePath, 0.42);
        ctx.lineWidth = 1.5;
        ctx.setLineDash([6, 10]);
        ctx.lineDashOffset = -pulse * 24;
        pathNodeIds.slice(0, -1).forEach((id, index) => {
          const edge = edgeLookup.get(`${id}->${pathNodeIds[index + 1]}`);
          if (!edge) {
            return;
          }
          ctx.beginPath();
          ctx.moveTo(edge.from.x, edge.from.y);
          ctx.lineTo(edge.to.x, edge.to.y);
          ctx.stroke();
        });
        ctx.setLineDash([]);
      };

      const drawNodes = () => {
        const pathSet = new Set(pathNodeIds);
        const goalId = pathNodeIds[pathNodeIds.length - 1];
        const goalNode = nodes.find((node) => node.id === goalId);
        if (!goalNode) {
          return null;
        }

        nodes.forEach((node) => {
          const onPath = pathSet.has(node.id);
          ctx.fillStyle = onPath ? toRgba(palette.nodePath, 0.34) : toRgba(palette.node, 0.22);
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.radius, 0, Math.PI * 2);
          ctx.fill();
        });

        ctx.strokeStyle = toRgba(palette.goal, 0.62);
        ctx.lineWidth = 1.6;
        ctx.beginPath();
        ctx.arc(goalNode.x, goalNode.y, 9 + Math.sin(pulse * 2.2) * 1.2, 0, Math.PI * 2);
        ctx.stroke();

        ctx.fillStyle = toRgba(palette.goal, 0.36);
        ctx.beginPath();
        ctx.arc(goalNode.x, goalNode.y, 4.2, 0, Math.PI * 2);
        ctx.fill();

        return goalNode;
      };

      const drawFrontierSweep = () => {
        const x = width * (0.1 + ((pulse * 0.08) % 0.82));
        const band = ctx.createLinearGradient(x - 48, 0, x + 48, 0);
        band.addColorStop(0, "rgba(0, 0, 0, 0)");
        band.addColorStop(0.5, toRgba(palette.sweep, 0.12));
        band.addColorStop(1, "rgba(0, 0, 0, 0)");
        ctx.fillStyle = band;
        ctx.fillRect(0, 0, width, height);
      };

      const updateAndDrawPackets = (dt) => {
        frontierTimer += dt;
        while (frontierTimer >= 150) {
          spawnPacket(false);
          if (Math.random() < 0.45) {
            spawnPacket(true);
          }
          frontierTimer -= 150;
        }

        packets = packets.filter((packet) => {
          packet.t += (dt / 1000) * packet.speed;
          if (packet.t >= 1) {
            return false;
          }
          const point = pointOnEdge(packet.edge, packet.t);
          const color = packet.hot ? palette.packet : palette.packetSoft;
          ctx.fillStyle = toRgba(color, packet.alpha);
          ctx.beginPath();
          ctx.arc(point.x, point.y, packet.radius, 0, Math.PI * 2);
          ctx.fill();
          return true;
        });
      };

      const drawStatic = () => {
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawEdges();
        const goalNode = drawNodes();
        if (goalNode) {
          drawHeuristicBands(goalNode);
        }
      };

      const drawFrame = (dt) => {
        pulse += dt / 1000;
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawFrontierSweep();
        drawEdges();
        const goalNode = drawNodes();
        if (goalNode) {
          drawHeuristicBands(goalNode);
        }
        updateAndDrawPackets(dt);
      };

      const tick = (timestamp) => {
        if (!lastFrame) {
          lastFrame = timestamp;
        }
        const dt = Math.min(34, Math.max(0, timestamp - lastFrame));
        lastFrame = timestamp;

        if (prefersReducedMotion.matches) {
          drawStatic();
          return;
        }

        drawFrame(dt);
        animationId = window.requestAnimationFrame(tick);
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
        updatePalette();
        buildGraph();
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }
        packets = [];
        frontierTimer = 0;
        lastFrame = 0;
        pulse = 0;
        for (let i = 0; i < 20; i += 1) {
          spawnPacket(i % 3 === 0);
        }

        if (prefersReducedMotion.matches) {
          drawStatic();
          return;
        }

        animationId = window.requestAnimationFrame(tick);
      };

      resize();
      start();

      window.addEventListener("resize", () => {
        resize();
        start();
      });

      const onMotionChange = () => {
        resize();
        start();
      };

      if (prefersReducedMotion.addEventListener) {
        prefersReducedMotion.addEventListener("change", onMotionChange);
      } else if (prefersReducedMotion.addListener) {
        prefersReducedMotion.addListener(onMotionChange);
      }

      const observer = new MutationObserver(() => {
        updatePalette();
      });
      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });
    })();
  </script>
</div>
