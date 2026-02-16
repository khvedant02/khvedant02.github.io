---
title: "Explainable Pathfinding for Inscrutable Planners with Inductive Logic Programming"
collection: publications
category: workshops
permalink: /publication/2022-icaps-explainable-pathfinding
excerpt: "An ILP-driven explainable pathfinding framework that summarizes solutions across all problem instances using an explainable pathfinding graph."
date: 2022-06-13
venue: 'ICAPS 2022 Workshop on Explainable AI Planning'
paperurl: "https://openreview.net/pdf?id=S44aSPW6lRa"
citation: 'Forest Agostinelli, Rojina Panta, Vedant Khandelwal, Biplav Srivastava, Bharath Chandra Muppasani, Kausik Lakkaraju, and Dezhi Wu. (2022). &quot;Explainable Pathfinding for Inscrutable Planners with Inductive Logic Programming.&quot; <i>ICAPS 2022 Workshop on Explainable AI Planning</i>.'
header:
  teaser: /images/publications/xplain/figure1.png
---

<div class="paper-xplain">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="xplain-egraph" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper explains pathfinding behavior across an entire domain by learning a compact, human-readable macro-action graph from planner outputs using inductive logic programming.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#xplain-why">Why</a>
      <a class="paper-jump-link" href="#xplain-what">What</a>
      <a class="paper-jump-link" href="#xplain-how">How</a>
      <a class="paper-jump-link" href="#xplain-key">Key contributions</a>
    </nav>

    <section id="xplain-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Modern planners (search, RL, neural methods) can solve pathfinding problems but cannot explain their solutions clearly.</li>
        <li>In many domains, human-understandable explanations are more important than optimal paths.</li>
        <li>Most explainable planning methods focus on explaining a single instance; this work explains all possible instances of a problem.</li>
        <li>Constraining solutions to an interpretable space improves trust, education, and knowledge transfer.</li>
      </ul>
    </section>

    <section id="xplain-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Introduced the <strong>Explainable Pathfinding Graph (e-graph)</strong> to represent solutions for all states in a domain.</li>
        <li>Represented nodes as first-order logic programs (state sets) and edges as macro-actions.</li>
        <li>Used <strong>Inductive Logic Programming (Popper)</strong> to learn human-understandable preconditions from planner-generated solutions.</li>
        <li>Defined explanation simplicity as minimizing total macro-action cost in the graph.</li>
        <li>Evaluated on 3-disk Towers of Hanoi (27 states), learning a 15-node graph, later compressed to 12 nodes, and finally to a 3-node hierarchical abstraction.</li>
      </ul>

      <figure class="paper-figure paper-figure-hierarchy">
        <img src="/images/publications/xplain/figure1.png" alt="Three-node hierarchical abstraction for Towers of Hanoi showing high-level logic over largest-disk states.">
        <figcaption>Figure 1. Final compressed hierarchy for Towers of Hanoi, showing that solutions can be summarized by reasoning about the largest disk.</figcaption>
      </figure>

      <p class="paper-reference">As shown in Figure 1, the explanation collapses to three high-level rules centered on the largest disk.</p>
    </section>

    <section id="xplain-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li>Initialize goal node as a logic program representing solved states.</li>
        <li>Generate sample states and use a planner rho (BFS for Towers of Hanoi) to extract macro-actions.</li>
        <li>Apply macro-actions to unsolved states to create positive and negative examples.</li>
        <li>Learn first-order logic preconditions using ILP to define new graph nodes.</li>
        <li>Greedily minimize explanation cost, measured as the sum of macro-action lengths.</li>
        <li>Post-process the graph into hierarchical or if/else explanations.</li>
      </ul>

      <figure class="paper-figure paper-figure-full">
        <img src="/images/publications/xplain/figure2.png" alt="Learned 15-node explainable pathfinding graph over logic-defined state clusters and macro-action transitions.">
        <figcaption>Figure 2. Learned explainable pathfinding graph before hierarchical compression.</figcaption>
      </figure>

      <p class="paper-reference">The initial e-graph (Figure 2) contains 15 logic-defined state clusters connected by macro-actions.</p>

      <figure class="paper-figure paper-figure-cost">
        <img src="/images/publications/xplain/figure3.png" alt="Comparison showing explanation-cost reduction when compositional macro-actions are used.">
        <figcaption>Figure 3. Illustration of graph cost reduction through compositional macro-actions.</figcaption>
      </figure>

      <p class="paper-reference">Figure 3 illustrates how compositionality reduces total explanation cost.</p>
    </section>

    <section id="xplain-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduces the <strong>e-graph framework</strong> for explaining solutions to all instances of a pathfinding problem.</li>
        <li>Formalizes explanation simplicity as a graph cost minimization objective.</li>
        <li>Integrates ILP (Popper) with an arbitrary planner to induce explainable macro-level structure.</li>
        <li>Demonstrates hierarchical abstraction and rule-based compression on Towers of Hanoi (27-state domain).</li>
        <li>Discusses extension to Rubik's Cube using DeepCubeA and hindsight experience replay.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-xplain {
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

    html[data-theme="dark"] .paper-xplain {
      --paper-shadow: 0 16px 34px rgba(0, 0, 0, 0.33);
    }

    .paper-xplain .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-xplain .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.38;
    }

    .paper-xplain .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-xplain .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-xplain .paper-jump-links {
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

    .paper-xplain .paper-jump-link {
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

    .paper-xplain .paper-jump-link:hover,
    .paper-xplain .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-xplain .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-xplain .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-xplain .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-xplain .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-xplain .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-xplain .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-xplain .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-xplain .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-xplain .paper-figure-full img,
    .paper-xplain .paper-figure-hierarchy img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.6rem;
    }

    html[data-theme="dark"] .paper-xplain .paper-figure-full img,
    html[data-theme="dark"] .paper-xplain .paper-figure-hierarchy img {
      border: 1px solid rgba(255, 255, 255, 0.16);
    }

    .paper-xplain .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-xplain .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-xplain .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-xplain .paper-jump-links {
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

      .paper-xplain .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-xplain .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-xplain .paper-section {
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

      const canvas = document.getElementById("xplain-egraph");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

      const CYCLE_MS = 12000;
      const FULL_MS = 4200;
      const COMPRESS_MS = 1800;
      const HIER_MS = 4200;
      const EXPAND_MS = 1800;

      let width = 0;
      let height = 0;
      let dpr = 1;
      let palette = null;
      let fullNodes = [];
      let fullEdges = [];
      let hierarchyNodes = [];
      let hierarchyEdges = [];
      let fullPackets = [];
      let hierarchyPackets = [];
      let animationId = null;
      let lastFrame = 0;
      let spawnFullTimer = 0;
      let spawnHierarchyTimer = 0;

      const clamp = (value, min, max) => Math.max(min, Math.min(max, value));
      const rand = (min, max) => min + Math.random() * (max - min);

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
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [76, 152, 173];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [52, 56, 63];

        palette = {
          wash: mixColor(bg, accent, 0.26),
          fullEdge: mixColor(bg, text, 0.42),
          fullNode: mixColor(bg, text, 0.58),
          hierarchyEdge: mixColor(bg, accent, 0.78),
          hierarchyNode: mixColor(bg, accent, 0.92),
          packetFull: mixColor(bg, text, 0.74),
          packetHierarchy: mixColor(bg, accent, 0.96),
          goalRing: mixColor(bg, accent, 0.66)
        };
      };

      const pointOnQuadratic = (p0, p1, p2, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * p0.x + 2 * inv * t * p1.x + t * t * p2.x,
          y: inv * inv * p0.y + 2 * inv * t * p1.y + t * t * p2.y
        };
      };

      const drawCurve = (curve) => {
        ctx.moveTo(curve.p0.x, curve.p0.y);
        ctx.quadraticCurveTo(curve.p1.x, curve.p1.y, curve.p2.x, curve.p2.y);
      };

      const makeCurve = (from, to, bend = 0) => {
        const midX = (from.x + to.x) * 0.5;
        const midY = (from.y + to.y) * 0.5 + bend;
        return { p0: from, p1: { x: midX, y: midY }, p2: to };
      };

      const buildGeometry = () => {
        const cols = [0.12, 0.285, 0.45, 0.615, 0.78];
        const rows = [0.24, 0.5, 0.76];

        fullNodes = [];
        cols.forEach((xRatio, col) => {
          rows.forEach((yRatio, row) => {
            fullNodes.push({
              id: `n-${col}-${row}`,
              col,
              row,
              x: xRatio * width,
              y: yRatio * height,
              radius: rand(2.9, 3.7)
            });
          });
        });

        const byId = new Map(fullNodes.map((node) => [node.id, node]));
        fullEdges = [];
        for (let col = 0; col < cols.length - 1; col += 1) {
          for (let row = 0; row < rows.length; row += 1) {
            const from = byId.get(`n-${col}-${row}`);
            [-1, 0, 1].forEach((delta) => {
              const nextRow = row + delta;
              if (nextRow < 0 || nextRow >= rows.length) {
                return;
              }
              const to = byId.get(`n-${col + 1}-${nextRow}`);
              const bend = delta === 0 ? 0 : delta * 18;
              fullEdges.push({
                from,
                to,
                curve: makeCurve(from, to, bend)
              });
            });
          }
        }

        hierarchyNodes = [
          { id: "h-left", x: width * 0.27, y: height * 0.72, radius: 8.5 },
          { id: "h-mid", x: width * 0.5, y: height * 0.34, radius: 9.2 },
          { id: "h-right", x: width * 0.73, y: height * 0.72, radius: 8.5 }
        ];

        hierarchyEdges = [
          {
            from: hierarchyNodes[0],
            to: hierarchyNodes[1],
            curve: makeCurve(hierarchyNodes[0], hierarchyNodes[1], -34)
          },
          {
            from: hierarchyNodes[1],
            to: hierarchyNodes[2],
            curve: makeCurve(hierarchyNodes[1], hierarchyNodes[2], -34)
          },
          {
            from: hierarchyNodes[0],
            to: hierarchyNodes[2],
            curve: makeCurve(hierarchyNodes[0], hierarchyNodes[2], 58)
          }
        ];
      };

      const getPhaseAlphas = (time) => {
        const t = time % CYCLE_MS;
        if (t < FULL_MS) {
          return { full: 1, hierarchy: 0 };
        }
        if (t < FULL_MS + COMPRESS_MS) {
          const k = (t - FULL_MS) / COMPRESS_MS;
          return { full: 1 - k, hierarchy: k };
        }
        if (t < FULL_MS + COMPRESS_MS + HIER_MS) {
          return { full: 0, hierarchy: 1 };
        }
        const k = (t - (FULL_MS + COMPRESS_MS + HIER_MS)) / EXPAND_MS;
        return { full: k, hierarchy: 1 - k };
      };

      const spawnFullPacket = () => {
        const edge = fullEdges[Math.floor(rand(0, fullEdges.length))];
        if (!edge) {
          return;
        }
        fullPackets.push({
          edge,
          t: 0,
          duration: rand(980, 1680),
          radius: rand(1.5, 2.2),
          alpha: rand(0.24, 0.42)
        });
      };

      const spawnHierarchyPacket = () => {
        const edge = hierarchyEdges[Math.floor(rand(0, hierarchyEdges.length))];
        if (!edge) {
          return;
        }
        hierarchyPackets.push({
          edge,
          t: 0,
          duration: rand(1160, 1720),
          radius: rand(2.4, 3.1),
          alpha: rand(0.26, 0.44)
        });
      };

      const drawBackdrop = () => {
        const gradient = ctx.createRadialGradient(
          width * 0.5,
          height * 0.5,
          28,
          width * 0.5,
          height * 0.5,
          Math.max(width, height) * 0.72
        );
        gradient.addColorStop(0, toRgba(palette.wash, 0.09));
        gradient.addColorStop(1, "rgba(0, 0, 0, 0)");
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, width, height);
      };

      const drawFullGraph = (alpha, nowTime) => {
        if (alpha <= 0.001) {
          return;
        }

        ctx.lineCap = "round";
        ctx.strokeStyle = toRgba(palette.fullEdge, 0.12 + alpha * 0.2);
        ctx.lineWidth = 1.1;
        fullEdges.forEach((edge) => {
          ctx.beginPath();
          drawCurve(edge.curve);
          ctx.stroke();
        });

        fullNodes.forEach((node) => {
          ctx.fillStyle = toRgba(palette.fullNode, 0.2 + alpha * 0.3);
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.radius, 0, Math.PI * 2);
          ctx.fill();
        });

        const goal = fullNodes.find((node) => node.id === "n-4-1");
        if (goal) {
          const pulse = (Math.sin(nowTime * 0.003) + 1) * 0.5;
          ctx.strokeStyle = toRgba(palette.goalRing, 0.12 + pulse * 0.2 * alpha);
          ctx.lineWidth = 1.4;
          ctx.beginPath();
          ctx.arc(goal.x, goal.y, 9 + pulse * 6, 0, Math.PI * 2);
          ctx.stroke();
        }
      };

      const drawHierarchyGraph = (alpha) => {
        if (alpha <= 0.001) {
          return;
        }

        ctx.strokeStyle = toRgba(palette.hierarchyEdge, 0.2 + alpha * 0.42);
        ctx.lineWidth = 2.2;
        hierarchyEdges.forEach((edge) => {
          ctx.beginPath();
          drawCurve(edge.curve);
          ctx.stroke();
        });

        hierarchyNodes.forEach((node) => {
          ctx.fillStyle = toRgba(palette.hierarchyNode, 0.18 + alpha * 0.36);
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.radius, 0, Math.PI * 2);
          ctx.fill();

          ctx.strokeStyle = toRgba(palette.hierarchyEdge, 0.2 + alpha * 0.52);
          ctx.lineWidth = 1.1;
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.radius + 6, 0, Math.PI * 2);
          ctx.stroke();
        });
      };

      const updateAndDrawPackets = (dt, fullAlpha, hierarchyAlpha) => {
        spawnFullTimer += dt;
        spawnHierarchyTimer += dt;

        while (spawnFullTimer >= 220) {
          spawnFullPacket();
          spawnFullTimer -= 220;
        }

        while (spawnHierarchyTimer >= 560) {
          spawnHierarchyPacket();
          spawnHierarchyTimer -= 560;
        }

        fullPackets = fullPackets.filter((packet) => {
          packet.t += dt / packet.duration;
          if (packet.t > 1) {
            return false;
          }
          const point = pointOnQuadratic(packet.edge.curve.p0, packet.edge.curve.p1, packet.edge.curve.p2, packet.t);
          ctx.fillStyle = toRgba(palette.packetFull, packet.alpha * fullAlpha);
          ctx.beginPath();
          ctx.arc(point.x, point.y, packet.radius, 0, Math.PI * 2);
          ctx.fill();
          return true;
        });

        hierarchyPackets = hierarchyPackets.filter((packet) => {
          packet.t += dt / packet.duration;
          if (packet.t > 1) {
            return false;
          }
          const point = pointOnQuadratic(packet.edge.curve.p0, packet.edge.curve.p1, packet.edge.curve.p2, packet.t);
          ctx.fillStyle = toRgba(palette.packetHierarchy, packet.alpha * hierarchyAlpha);
          ctx.beginPath();
          ctx.arc(point.x, point.y, packet.radius, 0, Math.PI * 2);
          ctx.fill();
          return true;
        });
      };

      const drawCompressionSweep = (fullAlpha, hierarchyAlpha) => {
        const blend = clamp(1 - Math.abs(fullAlpha - hierarchyAlpha), 0, 1);
        if (blend <= 0.01) {
          return;
        }
        const bandX = width * (0.18 + blend * 0.64);
        const gradient = ctx.createLinearGradient(bandX - 60, 0, bandX + 60, 0);
        gradient.addColorStop(0, "rgba(0, 0, 0, 0)");
        gradient.addColorStop(0.5, toRgba(palette.hierarchyEdge, 0.14 * blend));
        gradient.addColorStop(1, "rgba(0, 0, 0, 0)");
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, width, height);
      };

      const drawFrame = (nowTime, dt) => {
        const phase = getPhaseAlphas(nowTime);
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawFullGraph(phase.full, nowTime);
        drawHierarchyGraph(phase.hierarchy);
        drawCompressionSweep(phase.full, phase.hierarchy);
        updateAndDrawPackets(dt, phase.full, phase.hierarchy);
      };

      const drawStatic = () => {
        const staticTime = FULL_MS + COMPRESS_MS + HIER_MS * 0.4;
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawFullGraph(0.24, staticTime);
        drawHierarchyGraph(0.7);
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

        drawFrame(timestamp, dt);
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
        buildGeometry();
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }
        fullPackets = [];
        hierarchyPackets = [];
        spawnFullTimer = 0;
        spawnHierarchyTimer = 0;
        lastFrame = 0;

        if (prefersReducedMotion.matches) {
          drawStatic();
          return;
        }

        for (let i = 0; i < 18; i += 1) {
          spawnFullPacket();
        }
        for (let i = 0; i < 5; i += 1) {
          spawnHierarchyPacket();
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
        if (prefersReducedMotion.matches) {
          drawStatic();
        }
      });
      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });
    })();
  </script>
</div>
