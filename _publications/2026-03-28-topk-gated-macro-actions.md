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
  <div class="paper-bg" aria-hidden="true"></div>

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
        <li>Show on sliding-tile puzzles that <strong>K = 1</strong> reduces node expansions by up to <strong>29%</strong> on the 8-puzzle, <strong>18%</strong> on the 15-puzzle, and <strong>9%</strong> on the 24-puzzle.</li>
        <li>Find that random macros provide less than <strong>3%</strong> improvement, indicating the gains come from learned macro structure rather than simply adding longer actions.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/topk-gated-macros/figure1-pipeline.svg" alt="Pipeline showing macro discovery during approximate value iteration, training integration through macro landing states, and top-K gated search at inference.">
        <figcaption>Figure 1. End-to-end pipeline: macro discovery during training and top-K gated search at inference.</figcaption>
      </figure>

      <div class="paper-metric-grid" aria-label="Headline empirical results">
        <div class="paper-metric-card">
          <span class="paper-metric-value">29%</span>
          <span class="paper-metric-label">8-puzzle expansion reduction</span>
        </div>
        <div class="paper-metric-card">
          <span class="paper-metric-value">18%</span>
          <span class="paper-metric-label">15-puzzle expansion reduction</span>
        </div>
        <div class="paper-metric-card">
          <span class="paper-metric-value">9%</span>
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
        <li>Show that <strong>learned macros outperform random ones</strong>, with learned gating giving up to 29% lower expansions versus less than 3% for random macros.</li>
        <li>Demonstrate that <strong>K = 1 is Pareto-optimal</strong>, matching larger K with minimal branching overhead.</li>
        <li>Analyze when lower expansions do and do not translate to faster wall-clock runtime, with observed changes ranging from <strong>21% faster</strong> to <strong>11% slower</strong>.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table 1: Node expansion reductions with K equals 1 top-K gating">
          <table class="paper-table">
            <thead>
              <tr>
                <th>Puzzle</th>
                <th>Learned macros with K = 1</th>
                <th>Random macros</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>8-puzzle</td>
                <td>Up to 29% fewer node expansions</td>
                <td>Less than 3% improvement</td>
              </tr>
              <tr>
                <td>15-puzzle</td>
                <td>Up to 18% fewer node expansions</td>
                <td>Less than 3% improvement</td>
              </tr>
              <tr>
                <td>24-puzzle</td>
                <td>Up to 9% fewer node expansions</td>
                <td>Less than 3% improvement</td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table 1. Node expansion reductions across puzzles showing consistent gains with K = 1 gating.</figcaption>
      </figure>

      <p class="paper-reference">Table 1 shows that K = 1 consistently reduces expansions across domains.</p>
    </section>
  </div>

  <style>
    .paper-topk-macros {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-border: var(--global-border-color);
      --paper-panel: var(--global-bg-color);
      --paper-accent: #d97706;
      --paper-accent-soft: #0891b2;
      --paper-shadow: 0 14px 32px rgba(15, 23, 42, 0.12);
      --paper-table-even: rgba(15, 23, 42, 0.04);
      --paper-table-border: var(--global-border-color);
    }

    html[data-theme="dark"] .paper-topk-macros {
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.34);
      --paper-table-even: rgba(255, 255, 255, 0.06);
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
      border: 1px solid color-mix(in srgb, var(--paper-accent) 44%, var(--paper-border));
      background: color-mix(in srgb, var(--paper-accent) 10%, var(--paper-panel));
      color: color-mix(in srgb, var(--paper-accent) 88%, var(--paper-ink));
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
      background: color-mix(in srgb, var(--paper-panel) 80%, transparent);
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
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
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
      background: #ffffff;
      box-shadow: 0 14px 30px rgba(15, 23, 42, 0.14);
    }

    .paper-topk-macros .paper-figure figcaption {
      margin-top: 0.75rem;
      color: var(--paper-ink-soft);
      font-size: 0.92rem;
    }

    .paper-topk-macros .paper-reference {
      margin-top: 0.9rem;
      color: var(--paper-ink-soft);
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
      background: linear-gradient(180deg, color-mix(in srgb, var(--paper-panel) 92%, transparent), color-mix(in srgb, var(--paper-accent-soft) 10%, var(--paper-panel)));
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
      background: color-mix(in srgb, var(--paper-accent) 9%, var(--paper-panel));
    }

    .paper-topk-macros .paper-table-wrap {
      overflow-x: auto;
      border: 1px solid var(--paper-table-border);
      border-radius: 16px;
      background: var(--paper-panel);
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
      border-bottom: 1px solid var(--paper-table-border);
    }

    .paper-topk-macros .paper-table thead th {
      background: color-mix(in srgb, var(--paper-accent) 10%, var(--paper-panel));
      color: var(--paper-ink);
      font-weight: 700;
    }

    .paper-topk-macros .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-topk-macros .paper-table tbody tr:last-child td {
      border-bottom: 0;
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
</div>
