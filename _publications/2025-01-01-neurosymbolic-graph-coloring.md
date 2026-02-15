---
title: "A Neurosymbolic Fast and Slow Architecture for Graph Coloring"
collection: publications
category: conferences
permalink: /publication/2025-acs-neurosymbolic-graph-coloring
excerpt: "SOFAI-v2 combines fast LLM proposals with metacognitive verification and symbolic fallback for reliable graph coloring."
date: 2025-01-01
venue: "Twelfth Annual Conference on Advances in Cognitive Systems (ACS)"
paperurl: "http://www.cogsys.org/proceedings/2025/paper-2025-17.pdf"
codeurl: "https://github.com/khvedant02/CSP-SOFAI_v2"
citation: "Vedant Khandelwal, Vishal Pallagani, Biplav Srivastava, and Francesca Rossi. (2025). &quot;A Neurosymbolic Fast and Slow Architecture for Graph Coloring.&quot; <i>Twelfth Annual Conference on Advances in Cognitive Systems (ACS)</i>."
header:
  teaser: /images/publications/csp-sofai/figure1.png
---

<div class="paper-csp-sofai">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="csp-colorflow-bg" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">SOFAI-v2 combines fast LLM search with strict metacognitive checking and symbolic fallback to solve fixed-k graph coloring under exact constraint requirements.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#csp-why">Why</a>
      <a class="paper-jump-link" href="#csp-what">What</a>
      <a class="paper-jump-link" href="#csp-how">How</a>
      <a class="paper-jump-link" href="#csp-key">Key contributions</a>
    </nav>

    <section id="csp-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Constraint satisfaction problems require strict constraint adherence, but LLM-only solving is often unreliable on exactness requirements, while symbolic search can be slow.</li>
        <li>This work focuses on graph coloring in fixed-k decision form, where correctness is directly verifiable and supports systematic iterative guidance.</li>
        <li>The fast/slow setup addresses the practical gap between LLM speed and adaptability versus symbolic correctness on hard constraint-heavy instances.</li>
      </ul>
    </section>

    <section id="csp-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Introduced <strong>SOFAI-v2</strong>, extending SOFAI-v1 with iterative metacognitive governance over a fast solver (S1) and a slow fallback (S2).</li>
        <li><strong>S1 = Mistral-7B</strong> proposes candidate colorings; the metacognition module verifies each output with a polynomial-time correctness score based on edge conflicts.</li>
        <li>When incorrect, metacognition generates template-based feedback listing conflicting adjacent vertex pairs, and can add guiding examples with episodic-memory context for the next S1 attempt.</li>
        <li>If no improvement is observed after <strong>5</strong> iterations (or the score remains below threshold), the controller invokes <strong>S2 = DSATUR with backtracking</strong>.</li>
        <li>Under a strict <strong>200-second</strong> per-instance budget, evaluation reports a <strong>10.5%</strong> higher success rate and up to <strong>30%</strong> faster solving versus a traditional symbolic baseline, on instances up to <strong>50</strong> vertices.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/csp-sofai/figure1.png" alt="SOFAI-v2 architecture with metacognitive verification, iterative S1 feedback, and fallback to S2 DSATUR with backtracking.">
        <figcaption>Figure 1. SOFAI-v2's metacognitive controller verifies S1, iterates with feedback, and escalates to S2 when needed.</figcaption>
      </figure>

      <p class="paper-reference">The architecture diagram clarifies how verification and fallback are wired into the loop.</p>
    </section>

    <section id="csp-how" class="paper-section paper-anchor">
      <h2>How it works</h2>
      <ul class="paper-list">
        <li>S1 proposes a k-coloring (or <code>NOT SOLVABLE</code>) from a structured DIMACS prompt.</li>
        <li>Metacognition computes a constraint-adherence score by checking edge conflicts; only perfect adherence is accepted.</li>
        <li>If incorrect, metacognition generates template feedback listing conflicting adjacent vertex pairs.</li>
        <li>The controller can add simplified subgraph examples and retrieve similar past instances from episodic memory.</li>
        <li>If progress stalls across iterations, metacognition invokes S2 (DSATUR with backtracking) as fallback.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-figure-grid" role="group" aria-label="Figure 2: Iterative feedback impact across solvable, unsolvable, and mixed settings">
          <img src="/images/publications/csp-sofai/figure2a.png" alt="Figure 2a showing impact of metacognitive feedback iterations on solvable graph-coloring instances.">
          <img src="/images/publications/csp-sofai/figure2b.png" alt="Figure 2b showing impact of metacognitive feedback iterations on unsolvable graph-coloring instances.">
          <img src="/images/publications/csp-sofai/figure2c.png" alt="Figure 2c showing impact of metacognitive feedback iterations on mixed solvable-unsolvable graph-coloring instances.">
        </div>
        <figcaption>Figure 2. Iterative metacognitive feedback improves S1 success across solvable (a), unsolvable (b), and mixed (c) settings.</figcaption>
      </figure>

      <p class="paper-reference">The iteration plot shows why multiple feedback rounds matter, not just a single retry.</p>
    </section>

    <section id="csp-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>A SOFAI-v2 control loop coupling LLM proposals with polynomial-time verification and feedback.</li>
        <li>An episodic-memory retrieval mechanism to condition S1 with similar solved instances.</li>
        <li>An empirical study showing improved success rate and time efficiency versus S1, S2, and SOFAI-v1 baselines.</li>
        <li>An analysis of how iterative feedback rounds change success behavior across graph-size and solvability regimes.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table 2: Success rates across solvers by graph size and solvability mix">
          <table class="paper-table paper-table-wide">
            <thead>
              <tr>
                <th rowspan="2" scope="col" class="paper-col-size">Graph Size</th>
                <th colspan="4" scope="colgroup">m(100,0) [%]</th>
                <th colspan="4" scope="colgroup">m(0,100) [%]</th>
                <th colspan="4" scope="colgroup">m(50,50) [%]</th>
              </tr>
              <tr>
                <th scope="col">S1</th>
                <th scope="col">S2</th>
                <th scope="col">SOFAI-v1</th>
                <th scope="col">SOFAI-v2</th>
                <th scope="col">S1</th>
                <th scope="col">S2</th>
                <th scope="col">SOFAI-v1</th>
                <th scope="col">SOFAI-v2</th>
                <th scope="col">S1</th>
                <th scope="col">S2</th>
                <th scope="col">SOFAI-v1</th>
                <th scope="col">SOFAI-v2</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <th scope="row" class="paper-col-size">5</th>
                <td>9.41</td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td>75</td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td>45.36</td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
              </tr>
              <tr>
                <th scope="row" class="paper-col-size">10</th>
                <td>0</td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td>60.38</td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td>39.39</td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
                <td><strong>100</strong></td>
              </tr>
              <tr>
                <th scope="row" class="paper-col-size">15</th>
                <td>0</td>
                <td><strong>80</strong></td>
                <td><strong>80</strong></td>
                <td><strong>80</strong></td>
                <td>37.50</td>
                <td>77.08</td>
                <td>89.58</td>
                <td><strong>93.75</strong></td>
                <td>17.65</td>
                <td>77.45</td>
                <td>83.33</td>
                <td><strong>84.31</strong></td>
              </tr>
              <tr>
                <th scope="row" class="paper-col-size">20</th>
                <td>0</td>
                <td>5</td>
                <td>5</td>
                <td><strong>7.29</strong></td>
                <td>45.65</td>
                <td>4.35</td>
                <td>47.83</td>
                <td><strong>76.09</strong></td>
                <td>22.58</td>
                <td>3.06</td>
                <td>24.73</td>
                <td><strong>38.95</strong></td>
              </tr>
              <tr>
                <th scope="row" class="paper-col-size">30</th>
                <td>0</td>
                <td>0</td>
                <td>0</td>
                <td>0</td>
                <td>54.17</td>
                <td>0</td>
                <td>62.50</td>
                <td><strong>72.92</strong></td>
                <td>28.89</td>
                <td>0</td>
                <td>33.71</td>
                <td><strong>38.89</strong></td>
              </tr>
              <tr>
                <th scope="row" class="paper-col-size">40</th>
                <td>0</td>
                <td>0</td>
                <td>0</td>
                <td>0</td>
                <td>33.33</td>
                <td>0</td>
                <td><strong>47.37</strong></td>
                <td><strong>47.37</strong></td>
                <td>17.43</td>
                <td>0</td>
                <td>24.55</td>
                <td><strong>24.77</strong></td>
              </tr>
              <tr>
                <th scope="row" class="paper-col-size">50</th>
                <td>0</td>
                <td>0</td>
                <td>0</td>
                <td>0</td>
                <td>3.85</td>
                <td>0</td>
                <td>3.85</td>
                <td><strong>53.85</strong></td>
                <td>2.11</td>
                <td>0</td>
                <td>2.11</td>
                <td><strong>27.72</strong></td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table 2. Success-rate breakdown showing where SOFAI-v2 gains appear as size and solvability mix become harder.</figcaption>
      </figure>

      <p class="paper-reference">The success-rate table makes the gains most visible on larger, mixed, and unsat-heavy settings.</p>
    </section>
  </div>

  <style>
    .paper-csp-sofai {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-panel: var(--global-bg-color);
      --paper-border: var(--global-border-color);
      --paper-shadow: 0 14px 30px rgba(0, 0, 0, 0.12);
      --paper-accent: var(--global-link-color);
      --paper-accent-soft: var(--global-link-color-hover);
      --paper-table-even: rgba(0, 0, 0, 0.04);
      --paper-table-border: var(--global-border-color);
    }

    html[data-theme="dark"] .paper-csp-sofai {
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.35);
      --paper-table-even: rgba(255, 255, 255, 0.06);
    }

    .paper-csp-sofai .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-csp-sofai .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.36;
    }

    .paper-csp-sofai .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-csp-sofai .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-csp-sofai .paper-jump-links {
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

    .paper-csp-sofai .paper-jump-link {
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

    .paper-csp-sofai .paper-jump-link:hover,
    .paper-csp-sofai .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-csp-sofai .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-csp-sofai .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-csp-sofai .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-csp-sofai .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-csp-sofai .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), var(--paper-accent-soft));
    }

    .paper-csp-sofai .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-csp-sofai .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-csp-sofai .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-csp-sofai .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    html[data-theme="dark"] .paper-csp-sofai .paper-figure-architecture img {
      border: 1px solid rgba(255, 255, 255, 0.18);
    }

    .paper-csp-sofai .paper-figure-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 0.75rem;
    }

    .paper-csp-sofai .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-csp-sofai .paper-table-wrap {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .paper-csp-sofai .paper-table {
      width: 100%;
      min-width: 980px;
      border-collapse: collapse;
      font-size: 0.88rem;
    }

    .paper-csp-sofai .paper-table th,
    .paper-csp-sofai .paper-table td {
      border: 1px solid var(--paper-table-border);
      padding: 0.5rem 0.45rem;
      text-align: center;
      vertical-align: middle;
    }

    .paper-csp-sofai .paper-table thead th {
      background: var(--global-link-color);
      color: var(--global-bg-color);
      font-weight: 700;
      border-bottom: 2px solid var(--paper-table-border);
    }

    .paper-csp-sofai .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-csp-sofai .paper-table .paper-col-size {
      min-width: 92px;
      text-align: left;
      font-weight: 700;
      padding-left: 0.65rem;
    }

    .paper-csp-sofai .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 960px) {
      .paper-csp-sofai .paper-figure-grid {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 720px) {
      .paper-csp-sofai .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-csp-sofai .paper-jump-links {
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

      .paper-csp-sofai .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-csp-sofai .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-csp-sofai .paper-section {
        padding: 1.2rem 1.1rem;
      }

      .paper-csp-sofai .paper-table {
        font-size: 0.82rem;
        min-width: 900px;
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

      const canvas = document.getElementById("csp-colorflow-bg");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

      const NODE_COUNT = 18;
      const COLOR_COUNT = 4;
      const EDGE_PROBABILITY = 0.24;
      const MAX_S1_ITERS = 5;
      const S1_STEP_MS = 360;
      const S2_STEP_MS = 460;
      const SOLVED_HOLD_MS = 1300;

      let width = 0;
      let height = 0;
      let dpr = 1;
      let palette = null;
      let graph = null;
      let conflictEdges = [];
      let pulses = [];
      let mode = "s1";
      let iteration = 0;
      let stallCount = 0;
      let bestConflicts = Number.POSITIVE_INFINITY;
      let accumulator = 0;
      let solvedHold = 0;
      let animationId = null;
      let lastFrame = 0;

      const rand = (min, max) => min + Math.random() * (max - min);
      const randInt = (min, max) => Math.floor(rand(min, max + 1));
      const clamp = (value, min, max) => Math.max(min, Math.min(max, value));

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
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [73, 145, 168];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [50, 56, 63];

        palette = {
          wash: mixColor(bg, accent, 0.24),
          edge: mixColor(bg, text, 0.34),
          edgeConflict: [220, 90, 68],
          edgeResolved: mixColor(bg, accent, 0.62),
          nodeRing: mixColor(bg, text, 0.42),
          nodeText: mixColor(bg, text, 0.8),
          chipActive: mixColor(bg, accent, 0.7),
          chipIdle: mixColor(bg, text, 0.28),
          chipText: mixColor(bg, text, 0.75),
          lane: mixColor(bg, accent, 0.32),
          conflictPulse: [224, 108, 82],
          resolvePulse: mixColor(bg, accent, 0.8),
          colors: [
            [81, 132, 225],
            [65, 168, 95],
            [220, 90, 68],
            [190, 134, 52]
          ]
        };
      };

      const createPositions = () => {
        const centerX = width * 0.5;
        const centerY = height * 0.54;
        const radiusX = width * 0.32;
        const radiusY = height * 0.26;

        return Array.from({ length: NODE_COUNT }, (_, index) => {
          const angle = (Math.PI * 2 * index) / NODE_COUNT + rand(-0.16, 0.16);
          const radial = rand(0.68, 1.02);
          return {
            x: centerX + Math.cos(angle) * radiusX * radial,
            y: centerY + Math.sin(angle) * radiusY * radial,
            color: randInt(0, COLOR_COUNT - 1)
          };
        });
      };

      const edgeKey = (a, b) => (a < b ? `${a}-${b}` : `${b}-${a}`);

      const ensureConnectivity = (nodes, edges) => {
        const existing = new Set(edges.map((edge) => edgeKey(edge.a, edge.b)));
        for (let i = 0; i < nodes.length; i += 1) {
          let neighbor = -1;
          let bestDist = Number.POSITIVE_INFINITY;
          for (let j = 0; j < nodes.length; j += 1) {
            if (i === j) {
              continue;
            }
            const key = edgeKey(i, j);
            if (existing.has(key)) {
              neighbor = -1;
              bestDist = 0;
              break;
            }
            const dx = nodes[i].x - nodes[j].x;
            const dy = nodes[i].y - nodes[j].y;
            const dist = dx * dx + dy * dy;
            if (dist < bestDist) {
              bestDist = dist;
              neighbor = j;
            }
          }
          if (neighbor >= 0) {
            const key = edgeKey(i, neighbor);
            existing.add(key);
            edges.push({ a: i, b: neighbor });
          }
        }
      };

      const buildGraph = () => {
        const nodes = createPositions();
        const edges = [];
        const maxDist = Math.min(width, height) * 0.47;

        for (let i = 0; i < nodes.length; i += 1) {
          for (let j = i + 1; j < nodes.length; j += 1) {
            const dx = nodes[i].x - nodes[j].x;
            const dy = nodes[i].y - nodes[j].y;
            const dist = Math.hypot(dx, dy);
            if (dist <= maxDist && Math.random() < EDGE_PROBABILITY) {
              edges.push({ a: i, b: j });
            }
          }
        }

        ensureConnectivity(nodes, edges);

        const adjacency = Array.from({ length: nodes.length }, () => []);
        edges.forEach((edge) => {
          adjacency[edge.a].push(edge.b);
          adjacency[edge.b].push(edge.a);
        });

        graph = { nodes, edges, adjacency };
      };

      const computeConflicts = () => {
        conflictEdges = graph.edges.filter(
          (edge) => graph.nodes[edge.a].color === graph.nodes[edge.b].color
        );
        return conflictEdges.length;
      };

      const conflictingNodes = () => {
        const set = new Set();
        conflictEdges.forEach((edge) => {
          set.add(edge.a);
          set.add(edge.b);
        });
        return Array.from(set);
      };

      const localConflictCount = (nodeIndex, color) => {
        let count = 0;
        graph.adjacency[nodeIndex].forEach((neighbor) => {
          if (graph.nodes[neighbor].color === color) {
            count += 1;
          }
        });
        return count;
      };

      const bestColorForNode = (nodeIndex) => {
        let best = Number.POSITIVE_INFINITY;
        let candidates = [];
        for (let color = 0; color < COLOR_COUNT; color += 1) {
          const score = localConflictCount(nodeIndex, color);
          if (score < best) {
            best = score;
            candidates = [color];
          } else if (score === best) {
            candidates.push(color);
          }
        }
        return candidates[randInt(0, candidates.length - 1)];
      };

      const assignColor = (nodeIndex, color, type) => {
        const node = graph.nodes[nodeIndex];
        if (node.color === color) {
          return;
        }
        node.color = color;
        pulses.push({
          node: nodeIndex,
          age: 0,
          duration: type === "s1" ? 420 : 620,
          type
        });
      };

      const randomS1Step = () => {
        const conflictsNow = conflictingNodes();
        const edits = conflictsNow.length > 0 ? randInt(1, 3) : 2;

        for (let i = 0; i < edits; i += 1) {
          const useConflictNode = conflictsNow.length > 0 && Math.random() < 0.7;
          const nodeIndex = useConflictNode
            ? conflictsNow[randInt(0, conflictsNow.length - 1)]
            : randInt(0, graph.nodes.length - 1);

          let nextColor;
          if (Math.random() < 0.45) {
            nextColor = randInt(0, COLOR_COUNT - 1);
          } else {
            const best = bestColorForNode(nodeIndex);
            nextColor = Math.random() < 0.3 ? randInt(0, COLOR_COUNT - 1) : best;
          }
          assignColor(nodeIndex, nextColor, "s1");
        }
      };

      const s2Step = () => {
        const conflictsNow = conflictingNodes();
        if (conflictsNow.length === 0) {
          return;
        }

        let target = conflictsNow[0];
        let worst = -1;

        conflictsNow.forEach((nodeIndex) => {
          const nodeScore = localConflictCount(nodeIndex, graph.nodes[nodeIndex].color);
          if (nodeScore > worst || (nodeScore === worst && Math.random() < 0.35)) {
            target = nodeIndex;
            worst = nodeScore;
          }
        });

        assignColor(target, bestColorForNode(target), "s2");
      };

      const resetController = () => {
        iteration = 0;
        stallCount = 0;
        mode = "s1";
        accumulator = 0;
        solvedHold = 0;
        bestConflicts = computeConflicts();

        if (bestConflicts === 0 && graph.edges.length > 0) {
          const edge = graph.edges[randInt(0, graph.edges.length - 1)];
          assignColor(edge.b, graph.nodes[edge.a].color, "s1");
          bestConflicts = computeConflicts();
        }
      };

      const advanceModel = (dt) => {
        pulses = pulses
          .map((pulse) => ({ ...pulse, age: pulse.age + dt }))
          .filter((pulse) => pulse.age <= pulse.duration);

        if (mode === "solved") {
          solvedHold -= dt;
          if (solvedHold <= 0) {
            buildGraph();
            resetController();
          }
          return;
        }

        accumulator += dt;

        if (mode === "s1") {
          while (accumulator >= S1_STEP_MS) {
            accumulator -= S1_STEP_MS;
            iteration += 1;
            randomS1Step();
            const conflicts = computeConflicts();

            if (conflicts === 0) {
              mode = "solved";
              solvedHold = SOLVED_HOLD_MS;
              return;
            }

            if (conflicts < bestConflicts) {
              bestConflicts = conflicts;
              stallCount = 0;
            } else {
              stallCount += 1;
            }

            if (iteration >= MAX_S1_ITERS || stallCount >= 2) {
              mode = "s2";
              accumulator = 0;
              break;
            }
          }
          return;
        }

        while (accumulator >= S2_STEP_MS) {
          accumulator -= S2_STEP_MS;
          s2Step();
          const conflicts = computeConflicts();
          if (conflicts === 0) {
            mode = "solved";
            solvedHold = SOLVED_HOLD_MS;
            return;
          }
        }
      };

      const drawRoundRect = (x, y, w, h, r) => {
        const radius = Math.min(r, w * 0.5, h * 0.5);
        ctx.beginPath();
        ctx.moveTo(x + radius, y);
        ctx.lineTo(x + w - radius, y);
        ctx.quadraticCurveTo(x + w, y, x + w, y + radius);
        ctx.lineTo(x + w, y + h - radius);
        ctx.quadraticCurveTo(x + w, y + h, x + w - radius, y + h);
        ctx.lineTo(x + radius, y + h);
        ctx.quadraticCurveTo(x, y + h, x, y + h - radius);
        ctx.lineTo(x, y + radius);
        ctx.quadraticCurveTo(x, y, x + radius, y);
        ctx.closePath();
      };

      const drawOverlay = () => {
        const left = 18;
        const top = 18;
        const panelW = Math.min(390, width * 0.52);
        const panelH = 62;

        drawRoundRect(left, top, panelW, panelH, 10);
        ctx.fillStyle = toRgba(palette.lane, 0.12);
        ctx.fill();
        ctx.strokeStyle = toRgba(palette.nodeRing, 0.28);
        ctx.lineWidth = 1;
        ctx.stroke();

        const chipY = top + 12;
        const chipH = 18;
        const chipPad = 9;
        const chipW = 112;

        const drawChip = (x, label, active) => {
          drawRoundRect(x, chipY, chipW, chipH, 9);
          ctx.fillStyle = toRgba(active ? palette.chipActive : palette.chipIdle, active ? 0.28 : 0.2);
          ctx.fill();
          ctx.strokeStyle = toRgba(active ? palette.chipActive : palette.chipIdle, 0.42);
          ctx.stroke();
          ctx.fillStyle = toRgba(palette.chipText, 0.9);
          ctx.font = "600 11px sans-serif";
          ctx.textBaseline = "middle";
          ctx.fillText(label, x + 10, chipY + chipH * 0.56);
        };

        drawChip(left + 10, "S1 iterate", mode === "s1");
        drawChip(left + 10 + chipW + chipPad, "MC verify", mode !== "solved");
        drawChip(left + 10 + (chipW + chipPad) * 2, "S2 fallback", mode === "s2");

        ctx.fillStyle = toRgba(palette.nodeText, 0.82);
        ctx.font = "500 11px sans-serif";
        ctx.fillText(`S1 rounds: ${iteration}/${MAX_S1_ITERS}`, left + 12, top + panelH - 11);
        ctx.fillText(`Conflicts: ${conflictEdges.length}`, left + 150, top + panelH - 11);

        if (mode === "solved") {
          ctx.fillStyle = toRgba(palette.resolvePulse, 0.95);
          ctx.fillText("Solved, resetting graph...", left + 244, top + panelH - 11);
        }
      };

      const drawScene = (now) => {
        ctx.clearRect(0, 0, width, height);

        const wash = ctx.createRadialGradient(
          width * 0.52,
          height * 0.52,
          24,
          width * 0.52,
          height * 0.52,
          Math.max(width, height) * 0.64
        );
        wash.addColorStop(0, toRgba(palette.wash, 0.1));
        wash.addColorStop(1, "rgba(0,0,0,0)");
        ctx.fillStyle = wash;
        ctx.fillRect(0, 0, width, height);

        const conflictSet = new Set(conflictEdges.map((edge) => edgeKey(edge.a, edge.b)));

        graph.edges.forEach((edge) => {
          const a = graph.nodes[edge.a];
          const b = graph.nodes[edge.b];
          const isConflict = conflictSet.has(edgeKey(edge.a, edge.b));

          ctx.beginPath();
          ctx.moveTo(a.x, a.y);
          ctx.lineTo(b.x, b.y);
          ctx.strokeStyle = isConflict
            ? toRgba(palette.edgeConflict, mode === "s2" ? 0.46 : 0.36)
            : toRgba(mode === "s2" ? palette.edgeResolved : palette.edge, 0.22);
          ctx.lineWidth = isConflict ? 1.8 : 1;
          ctx.stroke();
        });

        graph.nodes.forEach((node, index) => {
          const inConflict = conflictEdges.some((edge) => edge.a === index || edge.b === index);
          const color = palette.colors[node.color % palette.colors.length];

          if (inConflict) {
            ctx.beginPath();
            ctx.arc(node.x, node.y, 10.2 + Math.sin(now * 0.006 + index) * 0.8, 0, Math.PI * 2);
            ctx.strokeStyle = toRgba(palette.conflictPulse, 0.44);
            ctx.lineWidth = 1.2;
            ctx.stroke();
          }

          ctx.beginPath();
          ctx.arc(node.x, node.y, 7.2, 0, Math.PI * 2);
          ctx.fillStyle = toRgba(color, 0.9);
          ctx.fill();
          ctx.strokeStyle = toRgba(palette.nodeRing, 0.5);
          ctx.lineWidth = 1;
          ctx.stroke();
        });

        pulses.forEach((pulse) => {
          const node = graph.nodes[pulse.node];
          const t = pulse.age / pulse.duration;
          const radius = 8 + t * 14;
          const alpha = (1 - t) * (pulse.type === "s2" ? 0.38 : 0.28);
          ctx.beginPath();
          ctx.arc(node.x, node.y, radius, 0, Math.PI * 2);
          ctx.strokeStyle = toRgba(
            pulse.type === "s2" ? palette.resolvePulse : palette.conflictPulse,
            alpha
          );
          ctx.lineWidth = pulse.type === "s2" ? 1.8 : 1.2;
          ctx.stroke();
        });

        drawOverlay();
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
        buildGraph();
        resetController();
      };

      const stopAnimation = () => {
        if (animationId) {
          cancelAnimationFrame(animationId);
          animationId = null;
        }
      };

      const animate = (timestamp) => {
        if (!lastFrame) {
          lastFrame = timestamp;
        }
        const dt = clamp(timestamp - lastFrame, 0, 64);
        lastFrame = timestamp;

        advanceModel(dt);
        drawScene(timestamp);
        animationId = window.requestAnimationFrame(animate);
      };

      const start = () => {
        updatePalette();
        resize();
        stopAnimation();
        lastFrame = 0;

        if (prefersReducedMotion.matches) {
          drawScene(performance.now());
          return;
        }

        animationId = window.requestAnimationFrame(animate);
      };

      const onMotionChange = () => {
        start();
      };

      start();

      window.addEventListener("resize", () => {
        updatePalette();
        resize();
        if (prefersReducedMotion.matches) {
          drawScene(performance.now());
        }
      }, { passive: true });

      if (typeof prefersReducedMotion.addEventListener === "function") {
        prefersReducedMotion.addEventListener("change", onMotionChange);
      }

      const observer = new MutationObserver(() => {
        updatePalette();
        drawScene(performance.now());
      });
      observer.observe(document.documentElement, {
        attributes: true,
        attributeFilter: ["data-theme", "class"]
      });
    })();
  </script>
</div>
