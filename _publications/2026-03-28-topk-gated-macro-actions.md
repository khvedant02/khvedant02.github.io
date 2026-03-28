---
title: "Top-K Gated Macro-Actions for Neural Heuristic Search"
collection: publications
category: preprints
permalink: /publication/2026-socs-topk-gated-macro-actions
excerpt: "Top-K gating bounds macro branching in neural heuristic search while preserving completeness and reducing node expansions."
date: 2026-03-28
venue: "Under review at SOCS 2026"
citation: "Vedant Khandelwal et al. (2026). &quot;Top-K Gated Macro-Actions for Neural Heuristic Search.&quot; <i>Under review at SOCS 2026</i>."
header:
  teaser: /images/publications/topk-gated-macros/figure1-pipeline.svg
---
<div class="paper-topk-macros">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="topk-gated-field" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-status">Under review at SOCS 2026</p>
    <p class="paper-lede">This paper studies how to keep the depth-reduction benefits of macro-actions in neural heuristic search without paying the full branching-factor cost at every expansion.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#topk-why">Why</a>
      <a class="paper-jump-link" href="#topk-what">What</a>
      <a class="paper-jump-link" href="#topk-how">How</a>
      <a class="paper-jump-link" href="#topk-key">Key contributions</a>
    </nav>

    <section id="topk-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <p>Neural heuristic search reduces reliance on handcrafted heuristics, but it makes each node expansion more expensive because every extra successor often requires another neural network evaluation.</p>
      <p>Macro-actions can shorten search depth, yet they usually increase branching. The central problem is balancing the depth reduction macros provide against the cost of exploring more successors.</p>
    </section>

    <section id="topk-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Introduce <strong>top-K gating</strong>, which keeps all primitive actions but selects only the <strong>K</strong> best macro successors at each expansion.</li>
        <li>Bound branching to <strong>b + K</strong> regardless of macro-pool size while preserving completeness.</li>
        <li>Discover macros during approximate value iteration (AVI) and integrate them into training by adding their landing states.</li>
        <li>Show on sliding-tile puzzles that <strong>K = 1</strong> reduces node expansions by up to <strong>28.6%</strong> on the 8-puzzle, <strong>17.5%</strong> on the 15-puzzle, and <strong>9.4%</strong> on the 24-puzzle.</li>
        <li>Find that random macros provide less than <strong>3%</strong> improvement, indicating the gains come from learned macro structure rather than simply adding longer actions.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/topk-gated-macros/figure1-pipeline.svg" alt="End-to-end architecture showing data generation, AVI training, macro discovery, optional utility scoring, and top-K gated search.">
        <figcaption>Figure 1. End-to-end architecture. <strong>Left:</strong> DeepCubeA generates training data via backward walks from the goal and trains a cost-to-go heuristic <code>h_theta</code> via approximate value iteration (AVI). <strong>Center:</strong> periodically during training, GBFS trajectories under <code>h_theta</code> are mined for macro candidates. <strong>Right:</strong> at search time, the full learned macro pool is deployed via top-K gating. Utility scoring is an optional filtering step evaluated as an ablation. The trained <code>h_theta</code> is reused for both macro discovery and gating decisions; no retraining is required.</figcaption>
      </figure>

      <div class="paper-metric-grid" aria-label="Headline empirical results">
        <div class="paper-metric-card">
          <span class="paper-metric-value">28.6%</span>
          <span class="paper-metric-label">8-puzzle expansion reduction</span>
        </div>
        <div class="paper-metric-card">
          <span class="paper-metric-value">17.5%</span>
          <span class="paper-metric-label">15-puzzle expansion reduction</span>
        </div>
        <div class="paper-metric-card">
          <span class="paper-metric-value">9.4%</span>
          <span class="paper-metric-label">24-puzzle expansion reduction</span>
        </div>
        <div class="paper-metric-card">
          <span class="paper-metric-value">&lt;3%</span>
          <span class="paper-metric-label">random macro improvement</span>
        </div>
      </div>

      <p class="paper-reference">The overall pipeline is shown in Figure 1, where macro discovery and search are tightly coupled.</p>
    </section>

    <section id="topk-how" class="paper-section paper-anchor">
      <h2>How it works</h2>
      <ul class="paper-list">
        <li><strong>Macro discovery during training:</strong> mine action subsequences of length 2-5 from GBFS trajectories under the learned heuristic.</li>
        <li><strong>Training integration:</strong> add macro landing states into the AVI training distribution while keeping Bellman updates primitive-only.</li>
        <li><strong>Optional utility scoring:</strong> rank macro candidates using support, applicability, benefit, and branching penalty.</li>
        <li><strong>Top-K gating at search time:</strong> evaluate all valid macros but retain only the <strong>K</strong> lowest-heuristic successors.</li>
        <li><strong>Cost consistency:</strong> assign each macro a cost equal to its primitive length to preserve A* correctness.</li>
      </ul>

      <div class="paper-callout">
        <strong>Key design choice:</strong> primitives are never gated away. Top-K gating only filters macro successors, so the search remains complete while macro branching stays explicitly bounded.
      </div>
    </section>

    <section id="topk-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduce <strong>top-K gating</strong> that preserves completeness and caps branching at <strong>b + K</strong>.</li>
        <li>Propose a <strong>macro discovery pipeline integrated with AVI training</strong>.</li>
        <li>Show that <strong>learned macros outperform random ones</strong>, with learned gating giving up to 28.6% lower expansions versus less than 3% for random macros.</li>
        <li>Demonstrate that <strong>K = 1 is Pareto-optimal</strong>, matching larger K with minimal branching overhead.</li>
        <li>Analyze when lower expansions do and do not translate to faster wall-clock runtime, with observed changes ranging from <strong>21% faster</strong> to <strong>11% slower</strong>.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table 1: Mean node expansions with primitive search and gated K equals 1 search">
          <table class="paper-table">
            <thead>
              <tr>
                <th>Puzzle</th>
                <th>k</th>
                <th>Primitive</th>
                <th>Gated K = 1</th>
                <th>Delta %</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td class="paper-domain" rowspan="3">8-puz</td>
                <td>20</td>
                <td>5.5 +/- 0.12</td>
                <td>4.7 +/- 0.10</td>
                <td>-14.6</td>
              </tr>
              <tr>
                <td>50</td>
                <td>9.9 +/- 0.20</td>
                <td>7.7 +/- 0.16</td>
                <td>-22.2</td>
              </tr>
              <tr>
                <td>100</td>
                <td>16.4 +/- 0.28</td>
                <td>11.7 +/- 0.21</td>
                <td class="paper-best-cell">-28.6</td>
              </tr>
              <tr>
                <td class="paper-domain" rowspan="5">15-puz</td>
                <td>20</td>
                <td>6.6 +/- 0.15</td>
                <td>6.3 +/- 0.15</td>
                <td>-3.6</td>
              </tr>
              <tr>
                <td>50</td>
                <td>13.9 +/- 0.27</td>
                <td>12.2 +/- 0.23</td>
                <td>-12.1</td>
              </tr>
              <tr>
                <td>100</td>
                <td>29.5 +/- 1.85</td>
                <td>24.3 +/- 1.64</td>
                <td class="paper-best-cell">-17.5</td>
              </tr>
              <tr class="paper-row-alt">
                <td>200</td>
                <td>67.1 +/- 4.01</td>
                <td>56.7 +/- 4.03</td>
                <td>-15.5</td>
              </tr>
              <tr>
                <td>500</td>
                <td>149.2 +/- 8.16</td>
                <td>130.3 +/- 7.54</td>
                <td>-12.7</td>
              </tr>
              <tr>
                <td class="paper-domain" rowspan="5">24-puz</td>
                <td>20</td>
                <td>6.9 +/- 0.15</td>
                <td>6.7 +/- 0.15</td>
                <td>-3.2</td>
              </tr>
              <tr>
                <td>50</td>
                <td>15.8 +/- 0.34</td>
                <td>14.3 +/- 0.30</td>
                <td class="paper-best-cell">-9.4</td>
              </tr>
              <tr>
                <td>100</td>
                <td>35.3 +/- 0.92</td>
                <td>32.4 +/- 0.90</td>
                <td>-8.2</td>
              </tr>
              <tr class="paper-row-alt">
                <td>200</td>
                <td>103.3 +/- 3.55</td>
                <td>97.4 +/- 3.57</td>
                <td>-5.7</td>
              </tr>
              <tr>
                <td>500</td>
                <td>394.0 +/- 19.6</td>
                <td>401.0 +/- 19.3</td>
                <td class="paper-delta-positive">+1.8<sup>dagger</sup></td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table 1. Mean node expansions (x 10^3) over solved instances under BWAS (lambda = 1.0). Delta % is the relative change versus primitive search; the best result per domain is shaded.</figcaption>
      </figure>

      <p class="paper-table-note"><sup>dagger</sup> Solve rate improves from 36.4% to 38.4%, so the solved-instance mean regresses slightly even though more 24-puzzle instances are solved.</p>

      <p class="paper-reference">Table 1 shows that K = 1 consistently reduces expansions across tested 8-puzzle, 15-puzzle, and 24-puzzle settings, with the strongest reductions at k = 100 for the 8- and 15-puzzle and at k = 50 for the 24-puzzle.</p>
    </section>
  </div>

  <style>
    .paper-topk-macros {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-accent: #d97706;
      --paper-accent-soft: #0284c7;
      --paper-ink: color-mix(in srgb, var(--global-text-color) 96%, #111827);
      --paper-ink-soft: color-mix(in srgb, var(--global-text-color) 72%, var(--global-bg-color));
      --paper-border: color-mix(in srgb, var(--global-border-color) 78%, var(--paper-accent-soft) 22%);
      --paper-panel: color-mix(in srgb, var(--global-bg-color) 92%, #ffffff 8%);
      --paper-panel-strong: color-mix(in srgb, var(--global-bg-color) 84%, var(--paper-accent-soft) 16%);
      --paper-figure-bg: color-mix(in srgb, #ffffff 84%, var(--paper-accent-soft) 16%);
      --paper-shadow: 0 16px 34px rgba(15, 23, 42, 0.13);
      --paper-table-even: rgba(15, 23, 42, 0.045);
      --paper-table-border: color-mix(in srgb, var(--global-border-color) 78%, var(--paper-accent) 22%);
      --paper-positive: #0f766e;
      --paper-bg-opacity: 0.68;
    }

    html[data-theme="dark"] .paper-topk-macros {
      --paper-accent: #f59e0b;
      --paper-accent-soft: #38bdf8;
      --paper-ink: color-mix(in srgb, var(--global-text-color) 96%, #f8fafc);
      --paper-ink-soft: color-mix(in srgb, var(--global-text-color) 68%, #94a3b8);
      --paper-border: color-mix(in srgb, var(--global-border-color) 62%, var(--paper-accent-soft) 38%);
      --paper-panel: color-mix(in srgb, var(--global-bg-color) 88%, #0f172a 12%);
      --paper-panel-strong: color-mix(in srgb, var(--global-bg-color) 74%, var(--paper-accent-soft) 26%);
      --paper-figure-bg: color-mix(in srgb, #0f172a 84%, var(--paper-accent-soft) 16%);
      --paper-shadow: 0 20px 42px rgba(0, 0, 0, 0.36);
      --paper-table-even: rgba(255, 255, 255, 0.065);
      --paper-table-border: color-mix(in srgb, var(--global-border-color) 64%, var(--paper-accent) 36%);
      --paper-positive: #2dd4bf;
      --paper-bg-opacity: 0.8;
    }

    .paper-topk-macros .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background:
        radial-gradient(circle at 14% 18%, rgba(245, 158, 11, 0.12), transparent 26%),
        radial-gradient(circle at 85% 22%, rgba(8, 145, 178, 0.12), transparent 30%),
        radial-gradient(circle at 72% 74%, rgba(249, 115, 22, 0.08), transparent 26%);
    }

    .paper-topk-macros .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: var(--paper-bg-opacity);
    }

    .paper-topk-macros .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-topk-macros .paper-status {
      display: inline-flex;
      align-items: center;
      margin: 0 0 0.6rem;
      padding: 0.3rem 0.8rem;
      border-radius: 999px;
      border: 1px solid color-mix(in srgb, var(--paper-accent) 54%, var(--paper-border));
      background: color-mix(in srgb, var(--paper-accent) 14%, var(--paper-panel));
      color: color-mix(in srgb, var(--paper-accent) 92%, var(--paper-ink));
      font-size: 0.92rem;
      font-weight: 700;
      letter-spacing: 0.01em;
      text-transform: uppercase;
    }

    .paper-topk-macros .paper-lede {
      margin: 0 0 0.7rem;
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      max-width: 54rem;
    }

    .paper-topk-macros .paper-jump-links {
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
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: 0 8px 22px rgba(0, 0, 0, 0.16);
      backdrop-filter: blur(10px);
      z-index: 30;
    }

    .paper-topk-macros .paper-jump-link {
      display: block;
      border: 1px solid var(--paper-border);
      border-radius: 999px;
      background: var(--paper-panel);
      color: var(--paper-ink);
      padding: 0.35rem 0.75rem;
      font-size: 0.88rem;
      line-height: 1.2;
      text-decoration: none;
      transition: border-color 0.2s ease, color 0.2s ease, transform 0.2s ease;
      white-space: nowrap;
      flex: 0 0 auto;
    }

    .paper-topk-macros .paper-jump-link:hover,
    .paper-topk-macros .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      transform: translateX(-2px);
      outline: none;
    }

    .paper-topk-macros .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-topk-macros .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 18px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 88%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-topk-macros .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-topk-macros .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-topk-macros .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), var(--paper-accent-soft), transparent);
    }

    .paper-topk-macros .paper-section p:last-child {
      margin-bottom: 0;
    }

    .paper-topk-macros .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-topk-macros .paper-list li + li {
      margin-top: 0.6rem;
    }

    .paper-topk-macros .paper-figure {
      margin: 1.25rem 0 0;
    }

    .paper-topk-macros .paper-figure img {
      display: block;
      width: 100%;
      border-radius: 20px;
      border: 1px solid var(--paper-border);
      background: var(--paper-figure-bg);
      box-shadow: 0 14px 30px rgba(15, 23, 42, 0.14);
    }

    .paper-topk-macros .paper-figure figcaption {
      margin-top: 0.75rem;
      color: var(--paper-ink);
      font-size: 0.92rem;
    }

    .paper-topk-macros .paper-reference {
      margin-top: 0.9rem;
      color: var(--paper-ink);
      font-size: 0.95rem;
      font-style: italic;
    }

    .paper-topk-macros .paper-metric-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 0.85rem;
      margin-top: 1rem;
    }

    .paper-topk-macros .paper-metric-card {
      display: flex;
      flex-direction: column;
      gap: 0.35rem;
      padding: 1rem;
      border-radius: 16px;
      border: 1px solid color-mix(in srgb, var(--paper-accent-soft) 28%, var(--paper-border));
      background: linear-gradient(180deg, color-mix(in srgb, var(--paper-panel) 92%, transparent), color-mix(in srgb, var(--paper-accent-soft) 12%, var(--paper-panel)));
    }

    .paper-topk-macros .paper-metric-value {
      font-size: clamp(1.55rem, 2.2vw, 2rem);
      line-height: 1;
      font-weight: 800;
      color: var(--paper-accent);
    }

    .paper-topk-macros .paper-metric-label {
      color: var(--paper-ink-soft);
      font-size: 0.92rem;
    }

    .paper-topk-macros .paper-callout {
      margin-top: 1rem;
      padding: 1rem 1.05rem;
      border-left: 4px solid var(--paper-accent);
      border-radius: 14px;
      background: color-mix(in srgb, var(--paper-accent) 12%, var(--paper-panel));
    }

    .paper-topk-macros .paper-table-wrap {
      overflow-x: auto;
      border: 1px solid var(--paper-table-border);
      border-radius: 16px;
      background: var(--paper-panel-strong);
    }

    .paper-topk-macros .paper-table {
      width: 100%;
      border-collapse: collapse;
      min-width: 520px;
    }

    .paper-topk-macros .paper-table th,
    .paper-topk-macros .paper-table td {
      padding: 0.85rem 1rem;
      text-align: left;
      vertical-align: top;
      border-bottom: 1px solid var(--paper-table-border);
    }

    .paper-topk-macros .paper-table thead th {
      background: color-mix(in srgb, var(--paper-accent) 16%, var(--paper-panel));
      color: var(--paper-ink);
      font-weight: 700;
    }

    .paper-topk-macros .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-topk-macros .paper-table .paper-domain {
      font-weight: 700;
      white-space: nowrap;
    }

    .paper-topk-macros .paper-table .paper-row-alt td {
      background: color-mix(in srgb, var(--paper-accent-soft) 8%, var(--paper-panel));
    }

    .paper-topk-macros .paper-table .paper-best-cell {
      background: color-mix(in srgb, var(--paper-accent) 24%, var(--paper-panel));
      font-weight: 800;
    }

    .paper-topk-macros .paper-table .paper-delta-positive {
      color: var(--paper-positive);
      font-weight: 700;
    }

    .paper-topk-macros .paper-table tbody tr:last-child td {
      border-bottom: 0;
    }

    .paper-topk-macros .paper-table-note {
      margin: 0.7rem 0 0;
      color: var(--paper-ink-soft);
      font-size: 0.9rem;
    }

    @media (max-width: 1200px) {
      .paper-topk-macros .paper-jump-links {
        position: static;
        transform: none;
        width: 100%;
        margin: 0.9rem 0 1rem;
      }
    }

    @media (max-width: 760px) {
      .paper-topk-macros .paper-section {
        padding: 1.1rem 1rem;
      }

      .paper-topk-macros .paper-metric-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }
    }

    @media (max-width: 520px) {
      .paper-topk-macros .paper-metric-grid {
        grid-template-columns: 1fr;
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

      const canvas = document.getElementById("topk-gated-field");
      const container = document.querySelector(".paper-topk-macros");
      if (!canvas || !container) {
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
      const sample = (items) => items[Math.floor(Math.random() * items.length)];

      let width = 0;
      let height = 0;
      let dpr = 1;
      let nodesByDepth = [];
      let primitiveEdges = [];
      let macroEdgesBySource = new Map();
      let activeMacroEdges = [];
      let rejectedMacroEdges = [];
      let gateSources = [];
      let packets = [];
      let palette = null;
      let animationId = null;
      let lastFrame = 0;
      let primitiveSpawnTimer = 0;
      let macroSpawnTimer = 0;
      let retargetTimer = 0;
      let phase = 0;

      const parseColor = (value) => {
        if (!value) {
          return null;
        }
        const trimmed = value.trim();
        if (trimmed.startsWith("#")) {
          const hex = trimmed.slice(1);
          if (hex.length === 3) {
            return hex.split("").map((part) => parseInt(part + part, 16));
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

      const mixColor = (a, b, amount) =>
        a.map((value, index) => Math.round(value + (b[index] - value) * amount));

      const toRgba = (rgb, alpha) => `rgba(${rgb[0]}, ${rgb[1]}, ${rgb[2]}, ${alpha})`;

      const updatePalette = () => {
        const rootStyles = getComputedStyle(root);
        const styles = getComputedStyle(container);
        const bg = parseColor(rootStyles.getPropertyValue("--global-bg-color")) || [248, 250, 252];
        const text = parseColor(styles.getPropertyValue("--paper-ink")) || [31, 41, 55];
        const accent = parseColor(styles.getPropertyValue("--paper-accent")) || [217, 119, 6];
        const accentSoft = parseColor(styles.getPropertyValue("--paper-accent-soft")) || [2, 132, 199];

        palette = {
          wash: mixColor(bg, accentSoft, 0.15),
          washWarm: mixColor(bg, accent, 0.11),
          grid: mixColor(bg, text, 0.18),
          node: mixColor(bg, text, 0.42),
          nodeHot: mixColor(bg, accent, 0.74),
          primitive: mixColor(bg, accentSoft, 0.54),
          primitiveGlow: mixColor(bg, accentSoft, 0.78),
          macro: mixColor(bg, accent, 0.88),
          macroGlow: mixColor(bg, accent, 0.96),
          reject: mixColor(bg, text, 0.26),
          gateRing: mixColor(bg, accent, 0.68),
          gateHalo: mixColor(bg, accentSoft, 0.48),
          packetPrimitive: mixColor(bg, accentSoft, 0.76),
          packetMacro: mixColor(bg, accent, 0.94)
        };
      };

      const getControlPoint = (source, target, isMacro) => {
        const midX = (source.x + target.x) / 2;
        const midY = (source.y + target.y) / 2;
        const horizontal = target.x - source.x;
        const direction = source.y < height * 0.5 ? -1 : 1;
        const bend = isMacro ? clamp(horizontal * 0.16, 36, 96) * direction : clamp((target.y - source.y) * 0.16, -28, 28);
        return { x: midX, y: midY + bend };
      };

      const sampleQuadratic = (source, control, target, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * source.x + 2 * inv * t * control.x + t * t * target.x,
          y: inv * inv * source.y + 2 * inv * t * control.y + t * t * target.y
        };
      };

      const makeEdge = (source, target, isMacro, score = 0) => {
        const control = getControlPoint(source, target, isMacro);
        return { source, target, control, isMacro, score };
      };

      const buildGraph = () => {
        const depthCount = width < 640 ? 5 : width < 960 ? 6 : 7;
        const counts = depthCount === 5 ? [1, 3, 5, 5, 4] : depthCount === 6 ? [1, 3, 5, 6, 5, 4] : [1, 3, 5, 7, 6, 5, 4];

        nodesByDepth = [];
        primitiveEdges = [];
        macroEdgesBySource = new Map();

        for (let depth = 0; depth < depthCount; depth += 1) {
          const count = counts[depth];
          const x = lerp(width * 0.08, width * 0.92, depth / (depthCount - 1));
          const nodes = [];

          for (let index = 0; index < count; index += 1) {
            const spread = count === 1 ? 0 : index / (count - 1);
            const fan = (spread - 0.5) * height * clamp(0.5 - depth * 0.03, 0.22, 0.5);
            const swing = Math.sin(depth * 0.88 + index * 1.31) * height * 0.02;
            nodes.push({
              id: `${depth}-${index}`,
              depth,
              index,
              x,
              y: height * 0.5 + fan + swing,
              radius: depth === 0 ? 6.4 : depth === depthCount - 1 ? 4.8 : 4.2
            });
          }

          nodesByDepth.push(nodes);
        }

        for (let depth = 0; depth < nodesByDepth.length - 1; depth += 1) {
          const current = nodesByDepth[depth];
          const next = nodesByDepth[depth + 1];
          current.forEach((source) => {
            next
              .map((target) => ({ target, distance: Math.abs(target.y - source.y) }))
              .sort((a, b) => a.distance - b.distance)
              .slice(0, Math.min(2, next.length))
              .forEach(({ target }) => {
                primitiveEdges.push(makeEdge(source, target, false));
              });
          });
        }

        for (let depth = 0; depth < nodesByDepth.length - 2; depth += 1) {
          const current = nodesByDepth[depth];
          const far = nodesByDepth[depth + 2];
          current.forEach((source) => {
            const candidates = far
              .map((target) => {
                const closeness = 1 - Math.min(1, Math.abs(target.y - source.y) / (height * 0.42));
                return makeEdge(source, target, true, closeness * 0.72 + rand(0.08, 0.3));
              })
              .sort((a, b) => b.score - a.score)
              .slice(0, Math.min(3, far.length));
            macroEdgesBySource.set(source.id, candidates);
          });
        }

        packets = [];
        chooseGateSet(true);
      };

      const chooseGateSet = (seedPackets = false) => {
        activeMacroEdges = [];
        rejectedMacroEdges = [];
        gateSources = [];

        const depthPools = nodesByDepth.slice(0, -2).filter((nodes) => nodes.length > 0);
        const selectedSources = depthPools
          .map((nodes) => sample(nodes))
          .slice(0, width < 700 ? 3 : 4);

        selectedSources.forEach((source) => {
          const candidates = macroEdgesBySource.get(source.id);
          if (!candidates || !candidates.length) {
            return;
          }

          const ranked = candidates
            .slice()
            .sort((a, b) => (b.score + rand(-0.08, 0.08)) - (a.score + rand(-0.08, 0.08)));

          const best = ranked[0];
          activeMacroEdges.push(best);
          rejectedMacroEdges.push(...ranked.slice(1));
          gateSources.push(source);

          if (seedPackets) {
            packets.push({
              edge: best,
              macro: true,
              t: rand(0, 0.92),
              speed: rand(0.18, 0.26),
              radius: rand(2.4, 3.4),
              alpha: rand(0.62, 0.88)
            });
          }
        });
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

      const drawEdge = (edge, color, lineWidth, alpha, dashed = false) => {
        ctx.save();
        ctx.strokeStyle = toRgba(color, alpha);
        ctx.lineWidth = lineWidth;
        ctx.lineCap = "round";
        ctx.lineJoin = "round";
        if (dashed) {
          ctx.setLineDash([7, 7]);
        }
        ctx.beginPath();
        ctx.moveTo(edge.source.x, edge.source.y);
        ctx.quadraticCurveTo(edge.control.x, edge.control.y, edge.target.x, edge.target.y);
        ctx.stroke();
        ctx.restore();
      };

      const drawPacket = (packet) => {
        const point = sampleQuadratic(packet.edge.source, packet.edge.control, packet.edge.target, packet.t);
        const color = packet.macro ? palette.packetMacro : palette.packetPrimitive;

        ctx.save();
        ctx.fillStyle = toRgba(color, packet.alpha);
        ctx.shadowBlur = packet.macro ? 16 : 10;
        ctx.shadowColor = toRgba(color, packet.alpha * 0.9);
        ctx.beginPath();
        ctx.arc(point.x, point.y, packet.radius, 0, Math.PI * 2);
        ctx.fill();
        ctx.restore();
      };

      const drawNode = (node) => {
        const active = activeMacroEdges.some((edge) => edge.source.id === node.id || edge.target.id === node.id);
        const gated = gateSources.some((candidate) => candidate.id === node.id);
        const fill = active ? palette.nodeHot : palette.node;

        ctx.save();
        ctx.fillStyle = toRgba(fill, active ? 0.9 : 0.38);
        ctx.beginPath();
        ctx.arc(node.x, node.y, node.radius + (active ? 1.1 : 0), 0, Math.PI * 2);
        ctx.fill();

        if (gated) {
          const pulse = 0.5 + 0.5 * Math.sin(phase + node.depth * 0.9);
          ctx.strokeStyle = toRgba(palette.gateRing, 0.22 + pulse * 0.22);
          ctx.lineWidth = 1.8;
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.radius + 7 + pulse * 4, 0, Math.PI * 2);
          ctx.stroke();

          ctx.strokeStyle = toRgba(palette.gateHalo, 0.12 + pulse * 0.12);
          ctx.lineWidth = 5;
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.radius + 4.5, 0, Math.PI * 2);
          ctx.stroke();
        }

        ctx.restore();
      };

      const drawBackdrop = () => {
        ctx.clearRect(0, 0, width, height);

        const warm = ctx.createRadialGradient(width * 0.18, height * 0.22, 0, width * 0.18, height * 0.22, width * 0.34);
        warm.addColorStop(0, toRgba(palette.washWarm, 0.16));
        warm.addColorStop(1, toRgba(palette.washWarm, 0));
        ctx.fillStyle = warm;
        ctx.fillRect(0, 0, width, height);

        const cool = ctx.createRadialGradient(width * 0.84, height * 0.26, 0, width * 0.84, height * 0.26, width * 0.38);
        cool.addColorStop(0, toRgba(palette.wash, 0.14));
        cool.addColorStop(1, toRgba(palette.wash, 0));
        ctx.fillStyle = cool;
        ctx.fillRect(0, 0, width, height);

        nodesByDepth.forEach((nodes) => {
          if (!nodes.length) {
            return;
          }
          const x = nodes[0].x;
          ctx.strokeStyle = toRgba(palette.grid, 0.08);
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.moveTo(x, height * 0.08);
          ctx.lineTo(x, height * 0.9);
          ctx.stroke();
        });
      };

      const render = (timestamp = 0) => {
        const dt = lastFrame ? Math.min(34, timestamp - lastFrame) : 16;
        lastFrame = timestamp;
        phase += dt * 0.0022;

        drawBackdrop();

        rejectedMacroEdges.forEach((edge) => {
          drawEdge(edge, palette.reject, 1.2, 0.12, true);
        });

        primitiveEdges.forEach((edge) => {
          drawEdge(edge, palette.primitive, 1.35, 0.16);
        });

        activeMacroEdges.forEach((edge, index) => {
          const glow = 0.12 + 0.08 * (0.5 + 0.5 * Math.sin(phase * 1.2 + index));
          drawEdge(edge, palette.macroGlow, 7, glow);
          drawEdge(edge, palette.macro, 2.6, 0.56);
        });

        nodesByDepth.flat().forEach(drawNode);
        packets.forEach(drawPacket);
      };

      const step = (timestamp = 0) => {
        const dt = lastFrame ? Math.min(34, timestamp - lastFrame) : 16;
        primitiveSpawnTimer += dt;
        macroSpawnTimer += dt;
        retargetTimer += dt;

        if (retargetTimer > 2600) {
          chooseGateSet(false);
          retargetTimer = 0;
        }

        while (primitiveSpawnTimer > 170) {
          primitiveSpawnTimer -= 170;
          const edge = sample(primitiveEdges);
          if (edge) {
            packets.push({
              edge,
              macro: false,
              t: 0,
              speed: rand(0.32, 0.48),
              radius: rand(1.3, 2.1),
              alpha: rand(0.26, 0.46)
            });
          }
        }

        while (macroSpawnTimer > 380) {
          macroSpawnTimer -= 380;
          const edge = sample(activeMacroEdges);
          if (edge) {
            packets.push({
              edge,
              macro: true,
              t: 0,
              speed: rand(0.18, 0.26),
              radius: rand(2.2, 3.2),
              alpha: rand(0.58, 0.82)
            });
          }
        }

        packets = packets
          .map((packet) => ({
            ...packet,
            t: packet.t + packet.speed * (dt / 1000)
          }))
          .filter((packet) => packet.t < 1.02);

        render(timestamp);
        animationId = window.requestAnimationFrame(step);
      };

      const stop = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }
      };

      const start = () => {
        stop();
        lastFrame = 0;
        primitiveSpawnTimer = 0;
        macroSpawnTimer = 0;
        retargetTimer = 0;
        if (prefersReducedMotion.matches) {
          render(0);
          return;
        }
        animationId = window.requestAnimationFrame(step);
      };

      resize();
      start();

      window.addEventListener("resize", () => {
        resize();
        start();
      });

      const handleThemeChange = () => {
        updatePalette();
        render(lastFrame);
      };

      if (typeof prefersReducedMotion.addEventListener === "function") {
        prefersReducedMotion.addEventListener("change", start);
      } else if (typeof prefersReducedMotion.addListener === "function") {
        prefersReducedMotion.addListener(start);
      }

      const observer = new MutationObserver(() => {
        updatePalette();
        start();
      });
      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });

      document.addEventListener("visibilitychange", () => {
        if (document.hidden) {
          stop();
          return;
        }
        handleThemeChange();
        start();
      });
    })();
  </script>
</div>
