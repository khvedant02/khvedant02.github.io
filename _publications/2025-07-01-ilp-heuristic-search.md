---
title: "Inductive Logic Programming for Heuristic Search"
collection: publications
category: workshops
permalink: /publication/2025-ilp-heuristic-search
excerpt: "Learning explainable cost-to-go heuristics directly as logic programs for efficient A* search."
date: 2025-07-01
venue: "5th International Joint Conference on Learning & Reasoning 2025 and ICAPS 2025 Workshop PRL (Accepted at two places)"
paperurl: "https://prl-theworkshop.github.io/prl2025-icaps/papers/3.pdf"
slidesurl: "https://docs.google.com/presentation/d/1y90rD1wl12DISOosIIeo6S5BsnkWERWXVVlg4MN8PRk/edit?usp=sharing"
codeurl: "https://github.com/khvedant02/HeurSearchILP"
citation: "Rojina Panta*, Vedant Khandelwal*, Celeste Veronese, Amit Sheth, Daniele Meli, and Forest Agostinelli. (2025). &quot;Inductive Logic Programming for Heuristic Search.&quot; <i>5th International Joint Conference on Learning &amp; Reasoning (IJCLR 2025) and ICAPS 2025 Workshop on Planning and Reinforcement Learning (PRL)</i>. (* Equal contribution)"
header:
  teaser: /images/publications/heurilp/figure1.png
---

<div class="paper-heursearch-ilp">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="heursearch-field" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper learns cost-to-go heuristic functions as logic programs, combining interpretable symbolic structure with effective A* search performance.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#heur-why">Why</a>
      <a class="paper-jump-link" href="#heur-what">What</a>
      <a class="paper-jump-link" href="#heur-how">How</a>
      <a class="paper-jump-link" href="#heur-key">Key contributions</a>
    </nav>

    <section id="heur-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Heuristic search depends on accurate cost-to-go functions to efficiently solve pathfinding problems.</li>
        <li>Deep neural network heuristics are not explainable, making knowledge extraction difficult.</li>
        <li>It has not been shown how to learn heuristic functions represented as logic programs.</li>
        <li>Explainable heuristics could enable structured knowledge discovery from domains such as puzzles, robotics, or chemistry.</li>
        <li>Learning heuristics directly as logic programs may combine interpretability with search effectiveness.</li>
      </ul>
    </section>

    <section id="heur-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Propose an algorithm to learn cost-to-go heuristic functions as logic programs using dynamic programming and ILP.</li>
        <li>Use A* search (multi-step lookahead) to compute updated heuristic values instead of one-step Bellman updates.</li>
        <li>Represent the heuristic as a dictionary mapping cost-to-go values to learned logic programs.</li>
        <li>Introduce predicate reuse, where rules learned for smaller depths are reused to learn deeper cost-to-go rules.</li>
        <li>Evaluate on the 8-puzzle (181,440 solvable states), showing improved accuracy with larger samples (for example, median R² up to 0.6925 with 2,000 states) and up to 100% optimal solutions when used with A* (Table I).</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/heurilp/figure1.png" alt="Figure showing R² and MSE trends versus number of sampled states, with and without predicate reuse.">
        <figcaption>Figure 1. Heuristic accuracy improves as the number of sampled states increases, and predicate reuse consistently improves performance.</figcaption>
      </figure>

      <p class="paper-reference">As shown in Figure 1, increasing the number of sampled states improves R² and reduces MSE, with predicate reuse yielding more accurate heuristics in most settings.</p>
    </section>

    <section id="heur-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li>Represent the heuristic as a dictionary mapping cost-to-go values to logic programs.</li>
        <li>Use A* to compute updated path costs for sampled states (multi-step lookahead).</li>
        <li>Convert updated values into positive and negative ILP examples for a target cost-to-go.</li>
        <li>Learn a logic program for each depth using Popper.</li>
        <li>Reuse previously learned clauses as background knowledge to build higher-cost rules.</li>
      </ul>
    </section>

    <section id="heur-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduce an algorithm to learn heuristic functions as logic programs via dynamic programming and ILP.</li>
        <li>Propose predicate reuse to incrementally construct deeper cost-to-go rules.</li>
        <li>Show that increasing sample size improves heuristic accuracy (for example, median R² up to 0.6925 with 2,000 states).</li>
        <li>Demonstrate that learned heuristics achieve up to 100% optimal solutions under A* search (Table I).</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table I: A* performance with learned heuristic">
          <table class="paper-table">
            <thead>
              <tr>
                <th>States (hour/s)</th>
                <th>Predicate Reuse</th>
                <th>Len</th>
                <th>Nodes</th>
                <th>Secs</th>
                <th>Nodes/Sec</th>
                <th>Solved (%)</th>
                <th>Optimal (%)</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>181440 (1 hour)</td>
                <td>Yes</td>
                <td>17.27</td>
                <td>118.33</td>
                <td>155.58</td>
                <td>1.02</td>
                <td>90.0</td>
                <td>100.0</td>
              </tr>
              <tr>
                <td>181440 (0.5 hours)</td>
                <td>No</td>
                <td>17.73</td>
                <td>1357.49</td>
                <td>117.61</td>
                <td>11.65</td>
                <td>98.0</td>
                <td>100.0</td>
              </tr>
              <tr>
                <td>181440 (1 hour)</td>
                <td>No</td>
                <td>17.73</td>
                <td>1332.29</td>
                <td>132.59</td>
                <td>10.21</td>
                <td>98.0</td>
                <td>100.0</td>
              </tr>
              <tr>
                <td>181440 (2 hours)</td>
                <td>No</td>
                <td>17.73</td>
                <td>560.18</td>
                <td>97.54</td>
                <td>6.00</td>
                <td>98.0</td>
                <td>100.0</td>
              </tr>
              <tr>
                <td>181440 (4 hours)</td>
                <td>No</td>
                <td>17.73</td>
                <td>499.61</td>
                <td>111.39</td>
                <td>4.53</td>
                <td>98.0</td>
                <td>100.0</td>
              </tr>
              <tr>
                <td>181440 (8 hours)</td>
                <td>No</td>
                <td>17.73</td>
                <td>347.76</td>
                <td>91.18</td>
                <td>3.89</td>
                <td>98.0</td>
                <td>100.0</td>
              </tr>
              <tr>
                <td>181440 (120 hours)</td>
                <td>No</td>
                <td>17.92</td>
                <td>112.28</td>
                <td>90.43</td>
                <td>1.33</td>
                <td>100.0</td>
                <td>100.0</td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table I. Learned logic heuristics guide A* to high optimal solve rates.</figcaption>
      </figure>

      <p class="paper-reference">Table I shows that the learned heuristic achieves up to 100% optimal solutions (learned for 181,440 states).</p>
    </section>
  </div>

  <style>
    .paper-heursearch-ilp {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-border: var(--global-border-color);
      --paper-panel: var(--global-bg-color);
      --paper-accent: var(--global-link-color);
      --paper-shadow: 0 12px 28px rgba(0, 0, 0, 0.12);
      --paper-table-even: rgba(0, 0, 0, 0.04);
      --paper-table-border: var(--global-border-color);
    }

    html[data-theme="dark"] .paper-heursearch-ilp {
      --paper-shadow: 0 16px 34px rgba(0, 0, 0, 0.33);
      --paper-table-even: rgba(255, 255, 255, 0.06);
    }

    .paper-heursearch-ilp .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-heursearch-ilp .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.38;
    }

    .paper-heursearch-ilp .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-heursearch-ilp .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-heursearch-ilp .paper-jump-links {
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

    .paper-heursearch-ilp .paper-jump-link {
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

    .paper-heursearch-ilp .paper-jump-link:hover,
    .paper-heursearch-ilp .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-heursearch-ilp .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-heursearch-ilp .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-heursearch-ilp .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-heursearch-ilp .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-heursearch-ilp .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-heursearch-ilp .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-heursearch-ilp .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-heursearch-ilp .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      box-sizing: border-box;
      padding: 0.35rem;
    }

    html[data-theme="dark"] .paper-heursearch-ilp .paper-figure img {
      border: 1px solid rgba(255, 255, 255, 0.16);
    }

    .paper-heursearch-ilp .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-heursearch-ilp .paper-table-wrap {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .paper-heursearch-ilp .paper-table {
      width: 100%;
      min-width: 760px;
      border-collapse: collapse;
      font-size: 0.94rem;
    }

    .paper-heursearch-ilp .paper-table th,
    .paper-heursearch-ilp .paper-table td {
      border: 1px solid var(--paper-table-border);
      padding: 0.55rem 0.65rem;
      text-align: left;
    }

    .paper-heursearch-ilp .paper-table thead th {
      background: var(--global-link-color);
      color: var(--global-bg-color);
      font-weight: 700;
    }

    .paper-heursearch-ilp .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-heursearch-ilp .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-heursearch-ilp .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-heursearch-ilp .paper-jump-links {
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

      .paper-heursearch-ilp .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-heursearch-ilp .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-heursearch-ilp .paper-section {
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

      const canvas = document.getElementById("heursearch-field");
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
          nodePath: mixColor(bg, accent, 0.88),
          goal: mixColor(bg, accent, 0.95),
          packet: mixColor(bg, accent, 0.92),
          packetSoft: mixColor(bg, text, 0.68),
          ringNear: mixColor(bg, accent, 0.62),
          ringFar: mixColor(bg, text, 0.42),
          sweep: mixColor(bg, accent, 0.58)
        };
      };

      const buildGraph = () => {
        const cols = 8;
        const rows = 5;
        const xStart = width * 0.1;
        const xEnd = width * 0.9;
        const yStart = height * 0.2;
        const yEnd = height * 0.8;
        const dx = (xEnd - xStart) / (cols - 1);
        const dy = (yEnd - yStart) / (rows - 1);

        nodes = [];
        edges = [];
        edgeLookup = new Map();
        pathNodeIds = [];

        for (let c = 0; c < cols; c += 1) {
          for (let r = 0; r < rows; r += 1) {
            const jitterX = rand(-dx * 0.07, dx * 0.07);
            const jitterY = rand(-dy * 0.09, dy * 0.09);
            nodes.push({
              id: `${c}-${r}`,
              c,
              r,
              x: xStart + c * dx + jitterX,
              y: yStart + r * dy + jitterY,
              radius: rand(2.2, 3.3)
            });
          }
        }

        const nodeById = new Map(nodes.map((node) => [node.id, node]));
        const pathRows = [0, 1, 1, 2, 2, 3, 2, 2];
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

      const spawnPacket = (emphasizePath = false) => {
        let edge = null;

        if (emphasizePath || Math.random() < 0.58) {
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
          speed: rand(0.55, 0.95),
          radius: emphasizePath ? rand(2.2, 3.4) : rand(1.4, 2.4),
          alpha: emphasizePath ? rand(0.28, 0.44) : rand(0.16, 0.3),
          hot: emphasizePath || Math.random() < 0.32
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
        const rings = [140, 240, 340, 450];
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
          ctx.lineWidth = isPath ? 2.1 : 1;
          ctx.beginPath();
          ctx.moveTo(edge.from.x, edge.from.y);
          ctx.lineTo(edge.to.x, edge.to.y);
          ctx.stroke();
        });

        ctx.strokeStyle = toRgba(palette.edgePath, 0.4);
        ctx.lineWidth = 1.4;
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

        ctx.strokeStyle = toRgba(palette.goal, 0.6);
        ctx.lineWidth = 1.5;
        ctx.beginPath();
        ctx.arc(goalNode.x, goalNode.y, 9 + Math.sin(pulse * 2.2) * 1.2, 0, Math.PI * 2);
        ctx.stroke();

        ctx.fillStyle = toRgba(palette.goal, 0.36);
        ctx.beginPath();
        ctx.arc(goalNode.x, goalNode.y, 4.3, 0, Math.PI * 2);
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
          if (Math.random() < 0.42) {
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
        for (let i = 0; i < 18; i += 1) {
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
