---
title: "A Domain-Agnostic Neurosymbolic Approach for Big Social Data Analysis: Evaluating Mental Health Sentiment on Social Media during COVID-19"
collection: publications
category: conferences
permalink: /publication/2024-bigdata-mental-health-sentiment
excerpt: "A domain-agnostic neurosymbolic pipeline for large-scale COVID-era mental health sentiment analysis across depression, addiction, and anxiety."
date: 2024-12-01
venue: "IEEE International Conference on Big Data"
paperurl: "https://ieeexplore.ieee.org/document/10825174"
codeurl: "https://github.com/khvedant02/Neurosymbolic-Mental-Health-Monitoring-COVID19"
citation: 'Vedant Khandelwal, Manas Gaur, Ugur Kursuncu, Valerie Shalin, and Amit Sheth. (2024). &quot;A Domain-Agnostic Neurosymbolic Approach for Big Social Data Analysis: Evaluating Mental Health Sentiment on Social Media during COVID-19.&quot; <i>Proceedings of the IEEE International Conference on Big Data</i>.'
header:
  teaser: /images/publications/covid/figure1.png
---

<div class="paper-covid-neurosymbolic">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="covid-signal-flow" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper presents a domain-agnostic neurosymbolic framework for analyzing large-scale social media signals and monitoring depression, addiction, and anxiety during COVID-19.</p>
    <p class="paper-note"><a href="https://ieeexplore.ieee.org/document/10825174">Paper</a> | <a href="https://github.com/khvedant02/Neurosymbolic-Mental-Health-Monitoring-COVID19">Code</a></p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#covid-why">Why</a>
      <a class="paper-jump-link" href="#covid-what">What</a>
      <a class="paper-jump-link" href="#covid-how">How</a>
      <a class="paper-jump-link" href="#covid-key">Key contributions</a>
    </nav>

    <section id="covid-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Social media generates large-scale, rapidly evolving signals (about 12 billion tweets during COVID-19) that can inform mental health surveillance.</li>
        <li>Purely data-driven models struggle with emerging terms, including pandemic-specific slang, which limits near-real-time monitoring quality.</li>
        <li>Large language model baselines can require high computational cost (more than 6 to 8 hours to converge in reported experiments), reducing practical rapid adaptation.</li>
        <li>Public-health deployment needs both high accuracy and adaptability across depression, anxiety, and addiction signals.</li>
      </ul>
    </section>

    <section id="covid-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Proposed a domain-agnostic neurosymbolic framework that integrates Word2Vec with multiple knowledge bases, including DSM-5, DAO, UMLS, and DBpedia.</li>
        <li>Introduced SEDO to modulate tweet embeddings through a learned weight matrix formulated via a Sylvester equation.</li>
        <li>Trained classifiers on semantically filtered data (900M to 600M tweets) and evaluated binary tasks for depression, addiction, and anxiety.</li>
        <li>Achieved F1 scores above 92%, outperforming zero-shot LLM baselines (about 70% to 80% F1) while converging in 40 to 55 minutes.</li>
        <li>Validated robustness with triangulation and ablation studies, including a +5.03% F1 gain for depression after SEDO fine-tuning.</li>
      </ul>
    </section>

    <section id="covid-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li><strong>Semantic Gap Management (B1):</strong> Train domain-specific LDA and Word2Vec models; dynamically update lexicons with knowledge bases and neologisms.</li>
        <li><strong>Metadata Scoring (B2):</strong> Compute semantic mapping and proximity scores; normalize index scores as supervision signals.</li>
        <li><strong>SEDO-based Infusion:</strong> Solve a Sylvester equation to learn a weight matrix that aligns tweet and knowledge-base embedding spaces.</li>
        <li><strong>Adaptive Classification (B3):</strong> Train binary classifiers (for example, Balanced Random Forest) for depression, addiction, and anxiety.</li>
        <li><strong>Validation:</strong> Perform triangulation and ablation studies to measure robustness and component-level gains.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/covid/figure1.png" alt="Multi-stage architecture showing semantic gap management, metadata scoring, and SEDO-based adaptive classification.">
        <figcaption>Figure 1. Multi-stage neurosymbolic pipeline integrating semantic gap management, metadata scoring, and SEDO-based adaptive classification.</figcaption>
      </figure>

      <p class="paper-reference">The architecture (Figure 1) shows how knowledge infusion and embedding modulation interact across three stages.</p>
    </section>

    <section id="covid-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>A multi-stage neurosymbolic architecture that combines shallow and semi-deep knowledge infusion for dynamic social media analysis.</li>
        <li>Empirical results above 92% F1, with consistent gains over zero-shot LLM baselines (about 89% to 93.6% versus 70% to 80%).</li>
        <li>Demonstrated efficiency: 40 to 55 minute convergence versus more than 6 to 8 hours for LLM baselines under similar settings.</li>
        <li>Triangulation and ablation studies showing measurable SEDO and knowledge-integration effects (for example, +5.03% F1 for depression after fine-tuning).</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table I: Comparison with zero-shot LLM baselines">
          <table class="paper-table">
            <thead>
              <tr>
                <th>Category</th>
                <th>Model</th>
                <th>Precision</th>
                <th>Recall</th>
                <th>F1-Score</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Depression</td>
                <td>LLama</td>
                <td>74.23</td>
                <td>70.57</td>
                <td>72.34</td>
              </tr>
              <tr>
                <td>Depression</td>
                <td>Phi</td>
                <td>71.67</td>
                <td>66.42</td>
                <td>68.95</td>
              </tr>
              <tr>
                <td>Depression</td>
                <td>Mistral</td>
                <td>76.51</td>
                <td>71.38</td>
                <td>73.87</td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Depression</td>
                <td>Neurosymbolic</td>
                <td>90.45</td>
                <td>87.29</td>
                <td>88.84</td>
              </tr>
              <tr>
                <td>Addiction</td>
                <td>LLama</td>
                <td>77.24</td>
                <td>73.68</td>
                <td>75.42</td>
              </tr>
              <tr>
                <td>Addiction</td>
                <td>Phi</td>
                <td>73.32</td>
                <td>69.75</td>
                <td>71.49</td>
              </tr>
              <tr>
                <td>Addiction</td>
                <td>Mistral</td>
                <td>78.45</td>
                <td>74.67</td>
                <td>76.51</td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Addiction</td>
                <td>Neurosymbolic</td>
                <td>92.18</td>
                <td>88.36</td>
                <td>90.22</td>
              </tr>
              <tr>
                <td>Anxiety</td>
                <td>LLama</td>
                <td>78.56</td>
                <td>74.82</td>
                <td>76.66</td>
              </tr>
              <tr>
                <td>Anxiety</td>
                <td>Phi</td>
                <td>74.38</td>
                <td>70.61</td>
                <td>72.43</td>
              </tr>
              <tr>
                <td>Anxiety</td>
                <td>Mistral</td>
                <td>80.33</td>
                <td>76.89</td>
                <td>78.56</td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Anxiety</td>
                <td>Neurosymbolic</td>
                <td>93.25</td>
                <td>90.52</td>
                <td>91.85</td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table I. Comparison between neurosymbolic classifiers and zero-shot LLMs across mental health categories.</figcaption>
      </figure>

      <p class="paper-reference">As shown in Table I, the neurosymbolic approach consistently exceeds LLM performance in F1 score.</p>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table II: Impact of removing SEDO">
          <table class="paper-table">
            <thead>
              <tr>
                <th>Category</th>
                <th>Model</th>
                <th>Precision</th>
                <th>Recall</th>
                <th>F1-Score</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Depression</td>
                <td>NB</td>
                <td>84.85 <span class="paper-drop">(-24%)</span></td>
                <td>82.68 <span class="paper-drop">(-25%)</span></td>
                <td>83.75 <span class="paper-drop">(-27%)</span></td>
              </tr>
              <tr>
                <td>Depression</td>
                <td>RF</td>
                <td>91.98 <span class="paper-drop">(-28%)</span></td>
                <td>91.81 <span class="paper-drop">(-26%)</span></td>
                <td>91.89 <span class="paper-drop">(-23%)</span></td>
              </tr>
              <tr>
                <td>Depression</td>
                <td>BRF</td>
                <td>92.32 <span class="paper-drop">(-27%)</span></td>
                <td>92.43 <span class="paper-drop">(-24%)</span></td>
                <td>92.37 <span class="paper-drop">(-29%)</span></td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Depression</td>
                <td>BSRF</td>
                <td>94.12 <span class="paper-drop">(-29%)</span></td>
                <td>93.02 <span class="paper-drop">(-22%)</span></td>
                <td>93.57 <span class="paper-drop">(-28%)</span></td>
              </tr>

              <tr>
                <td>Addiction</td>
                <td>NB</td>
                <td>82.74 <span class="paper-drop">(-26%)</span></td>
                <td>80.46 <span class="paper-drop">(-21%)</span></td>
                <td>81.58 <span class="paper-drop">(-25%)</span></td>
              </tr>
              <tr>
                <td>Addiction</td>
                <td>RF</td>
                <td>90.02 <span class="paper-drop">(-22%)</span></td>
                <td>90.36 <span class="paper-drop">(-20%)</span></td>
                <td>90.19 <span class="paper-drop">(-23%)</span></td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Addiction</td>
                <td>BRF</td>
                <td>91.53 <span class="paper-drop">(-28%)</span></td>
                <td>91.78 <span class="paper-drop">(-26%)</span></td>
                <td>91.65 <span class="paper-drop">(-29%)</span></td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Addiction</td>
                <td>BSRF</td>
                <td>91.64 <span class="paper-drop">(-27%)</span></td>
                <td>91.82 <span class="paper-drop">(-24%)</span></td>
                <td>91.73 <span class="paper-drop">(-28%)</span></td>
              </tr>

              <tr>
                <td>Anxiety</td>
                <td>NB</td>
                <td>82.53 <span class="paper-drop">(-25%)</span></td>
                <td>81.87 <span class="paper-drop">(-24%)</span></td>
                <td>82.20 <span class="paper-drop">(-22%)</span></td>
              </tr>
              <tr>
                <td>Anxiety</td>
                <td>RF</td>
                <td>90.76 <span class="paper-drop">(-23%)</span></td>
                <td>92.78 <span class="paper-drop">(-28%)</span></td>
                <td>91.76 <span class="paper-drop">(-21%)</span></td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Anxiety</td>
                <td>BRF</td>
                <td>94.37 <span class="paper-drop">(-27%)</span></td>
                <td>93.87 <span class="paper-drop">(-25%)</span></td>
                <td>94.12 <span class="paper-drop">(-29%)</span></td>
              </tr>
              <tr>
                <td>Anxiety</td>
                <td>BSRF</td>
                <td>93.46 <span class="paper-drop">(-24%)</span></td>
                <td>93.85 <span class="paper-drop">(-27%)</span></td>
                <td>93.65 <span class="paper-drop">(-28%)</span></td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table II. Performance drop without SEDO highlights the contribution of embedding modulation (percentage decrease values shown in red).</figcaption>
      </figure>

      <p class="paper-reference">Table II quantifies the degradation when SEDO is removed, underscoring its impact.</p>
    </section>
  </div>

  <style>
    .paper-covid-neurosymbolic {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-ink-strong: var(--global-text-color);
      --paper-panel: var(--global-bg-color);
      --paper-panel-soft: var(--global-bg-color);
      --paper-border: var(--global-border-color);
      --paper-shadow: 0 14px 30px rgba(0, 0, 0, 0.12);
      --paper-accent: var(--global-link-color);
      --paper-table-even: rgba(0, 0, 0, 0.04);
      --paper-table-border: var(--global-border-color);
      --paper-table-head-bg: var(--global-link-color);
      --paper-table-head-ink: var(--global-bg-color);
      --paper-row-highlight: color-mix(in srgb, var(--paper-accent) 11%, transparent);
      --paper-drop: #b13030;
    }

    html[data-theme="dark"] .paper-covid-neurosymbolic {
      --paper-table-even: rgba(255, 255, 255, 0.06);
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.35);
      --paper-row-highlight: color-mix(in srgb, var(--paper-accent) 16%, transparent);
      --paper-drop: #ff8e8e;
    }

    .paper-covid-neurosymbolic .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-covid-neurosymbolic .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.37;
    }

    .paper-covid-neurosymbolic .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-covid-neurosymbolic .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.25rem;
    }

    .paper-covid-neurosymbolic .paper-note {
      margin-top: 0;
      color: var(--paper-ink-soft);
    }

    .paper-covid-neurosymbolic .paper-jump-links {
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

    .paper-covid-neurosymbolic .paper-jump-link {
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

    .paper-covid-neurosymbolic .paper-jump-link:hover,
    .paper-covid-neurosymbolic .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-covid-neurosymbolic .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-covid-neurosymbolic .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel-soft) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-covid-neurosymbolic .paper-section {
      background: color-mix(in srgb, var(--paper-panel-soft) 82%, transparent);
    }

    .paper-covid-neurosymbolic .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink-strong);
    }

    .paper-covid-neurosymbolic .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-covid-neurosymbolic .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-covid-neurosymbolic .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-covid-neurosymbolic .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-covid-neurosymbolic .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    html[data-theme="dark"] .paper-covid-neurosymbolic .paper-figure-architecture img {
      border: 1px solid rgba(255, 255, 255, 0.2);
    }

    .paper-covid-neurosymbolic .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-covid-neurosymbolic .paper-table-wrap {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .paper-covid-neurosymbolic .paper-table {
      width: 100%;
      min-width: 640px;
      border-collapse: collapse;
      font-size: 0.94rem;
    }

    .paper-covid-neurosymbolic .paper-table th,
    .paper-covid-neurosymbolic .paper-table td {
      border: 1px solid var(--paper-table-border);
      padding: 0.58rem 0.68rem;
      text-align: left;
      vertical-align: top;
    }

    .paper-covid-neurosymbolic .paper-table thead th {
      background: var(--paper-table-head-bg);
      color: var(--paper-table-head-ink);
      font-weight: 700;
      border-bottom: 2px solid var(--paper-table-border);
    }

    .paper-covid-neurosymbolic .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-covid-neurosymbolic .paper-row-highlight {
      background: var(--paper-row-highlight);
      font-weight: 600;
    }

    .paper-covid-neurosymbolic .paper-drop {
      color: var(--paper-drop);
      font-weight: 600;
    }

    .paper-covid-neurosymbolic .paper-reference {
      margin-top: 0;
      color: var(--paper-ink-strong);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-covid-neurosymbolic .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-covid-neurosymbolic .paper-jump-links {
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

      .paper-covid-neurosymbolic .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-covid-neurosymbolic .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-covid-neurosymbolic .paper-section {
        padding: 1.2rem 1.1rem;
      }

      .paper-covid-neurosymbolic .paper-table {
        font-size: 0.9rem;
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

      const canvas = document.getElementById("covid-signal-flow");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

      const sourceNode = { x: 0.14, y: 0.5 };
      const kbNodes = [
        { x: 0.48, y: 0.22 },
        { x: 0.56, y: 0.4 },
        { x: 0.5, y: 0.58 },
        { x: 0.6, y: 0.76 }
      ];
      const outputNodes = [
        { x: 0.86, y: 0.31 },
        { x: 0.86, y: 0.5 },
        { x: 0.86, y: 0.69 }
      ];

      let width = 0;
      let height = 0;
      let dpr = 1;
      let palette = null;
      let particles = [];
      let ripples = [];
      let animationId = null;
      let lastFrame = 0;
      let spawnTimer = 0;

      const rand = (min, max) => min + Math.random() * (max - min);
      const randInt = (min, max) => Math.floor(rand(min, max + 1));

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
        const bg = parseColor(styles.getPropertyValue("--global-bg-color")) || [241, 241, 241];
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [76, 135, 153];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [56, 60, 66];

        palette = {
          wash: mixColor(bg, accent, 0.25),
          source: mixColor(bg, text, 0.45),
          sourceSoft: mixColor(bg, text, 0.3),
          kb: mixColor(bg, accent, 0.56),
          kbSoft: mixColor(bg, accent, 0.36),
          output: mixColor(bg, accent, 0.74),
          outputSoft: mixColor(bg, text, 0.44),
          route: mixColor(bg, accent, 0.46),
          routeSoft: mixColor(bg, text, 0.3),
          particle: mixColor(bg, accent, 0.82),
          particleSoft: mixColor(bg, text, 0.56)
        };
      };

      const screenPoint = (node) => ({ x: node.x * width, y: node.y * height });

      const buildCurve = (start, end, curveAmount) => {
        const dx = end.x - start.x;
        const dy = end.y - start.y;
        const len = Math.max(1, Math.hypot(dx, dy));
        const nx = -dy / len;
        const ny = dx / len;
        const bend = curveAmount * len;
        return {
          p0: start,
          p1: { x: (start.x + end.x) * 0.5 + nx * bend, y: (start.y + end.y) * 0.5 + ny * bend },
          p2: end
        };
      };

      const pointOnCurve = (curve, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * curve.p0.x + 2 * inv * t * curve.p1.x + t * t * curve.p2.x,
          y: inv * inv * curve.p0.y + 2 * inv * t * curve.p1.y + t * t * curve.p2.y
        };
      };

      const drawCurve = (curve) => {
        ctx.moveTo(curve.p0.x, curve.p0.y);
        ctx.quadraticCurveTo(curve.p1.x, curve.p1.y, curve.p2.x, curve.p2.y);
      };

      const spawnRipple = (x, y, type) => {
        ripples.push({
          x,
          y,
          r: type === "output" ? 5 : 3.8,
          life: 0,
          ttl: type === "output" ? 980 : 760,
          alpha: type === "output" ? 0.34 : 0.24,
          type
        });
      };

      const spawnParticle = (seed = false) => {
        const kbIndex = randInt(0, kbNodes.length - 1);
        const outIndex = randInt(0, outputNodes.length - 1);
        particles.push({
          kbIndex,
          outIndex,
          phase: seed && Math.random() > 0.56 ? 1 : 0,
          t: seed ? Math.random() : 0,
          speed: rand(0.36, 0.54),
          size: rand(1.35, 2.45),
          alpha: rand(0.2, 0.42),
          wobble: rand(0, Math.PI * 2)
        });
      };

      const drawBackdrop = () => {
        const source = screenPoint(sourceNode);
        const radial = ctx.createRadialGradient(
          width * 0.56,
          height * 0.5,
          40,
          width * 0.56,
          height * 0.5,
          Math.max(width, height) * 0.76
        );
        radial.addColorStop(0, toRgba(palette.wash, 0.08));
        radial.addColorStop(1, "rgba(0,0,0,0)");
        ctx.fillStyle = radial;
        ctx.fillRect(0, 0, width, height);

        ctx.strokeStyle = toRgba(palette.sourceSoft, 0.1);
        ctx.lineWidth = 12;
        ctx.beginPath();
        ctx.moveTo(source.x, height * 0.08);
        ctx.lineTo(source.x, height * 0.92);
        ctx.stroke();
      };

      const drawRoutes = (time) => {
        const source = screenPoint(sourceNode);

        kbNodes.forEach((node, index) => {
          const kb = screenPoint(node);
          const sourceCurve = buildCurve(source, kb, index % 2 === 0 ? -0.14 : 0.14);
          ctx.setLineDash([5, 9]);
          ctx.strokeStyle = toRgba(palette.routeSoft, 0.2);
          ctx.lineWidth = 1.05;
          ctx.beginPath();
          drawCurve(sourceCurve);
          ctx.stroke();

          outputNodes.forEach((outputNode, outIndex) => {
            const output = screenPoint(outputNode);
            const sign = outIndex === 1 ? 0 : outIndex === 0 ? -1 : 1;
            const routeCurve = buildCurve(kb, output, sign * (0.09 + index * 0.01));
            ctx.setLineDash([]);
            ctx.strokeStyle = toRgba(palette.route, 0.1 + 0.04 * Math.sin(time * 0.001 + index + outIndex));
            ctx.lineWidth = 1.05;
            ctx.beginPath();
            drawCurve(routeCurve);
            ctx.stroke();
          });
        });

        ctx.setLineDash([]);
      };

      const drawNodes = (time) => {
        const source = screenPoint(sourceNode);
        const pulse = 0.5 + 0.5 * Math.sin(time * 0.0022);

        ctx.fillStyle = toRgba(palette.source, 0.36);
        ctx.beginPath();
        ctx.arc(source.x, source.y, 8, 0, Math.PI * 2);
        ctx.fill();

        ctx.strokeStyle = toRgba(palette.sourceSoft, 0.24 + pulse * 0.14);
        ctx.lineWidth = 1.1;
        ctx.beginPath();
        ctx.arc(source.x, source.y, 14 + pulse * 6, 0, Math.PI * 2);
        ctx.stroke();

        kbNodes.forEach((node, index) => {
          const kb = screenPoint(node);
          const localPulse = 0.5 + 0.5 * Math.sin(time * 0.002 + index * 1.2);
          ctx.fillStyle = toRgba(palette.kb, 0.3);
          ctx.beginPath();
          ctx.arc(kb.x, kb.y, 6.2, 0, Math.PI * 2);
          ctx.fill();

          ctx.strokeStyle = toRgba(palette.kbSoft, 0.2 + localPulse * 0.12);
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.arc(kb.x, kb.y, 11 + localPulse * 4, 0, Math.PI * 2);
          ctx.stroke();
        });

        outputNodes.forEach((node, index) => {
          const output = screenPoint(node);
          const localPulse = 0.5 + 0.5 * Math.sin(time * 0.0023 + index * 0.9);
          ctx.fillStyle = toRgba(palette.output, 0.33);
          ctx.beginPath();
          ctx.arc(output.x, output.y, 7.2, 0, Math.PI * 2);
          ctx.fill();

          ctx.strokeStyle = toRgba(palette.outputSoft, 0.24 + localPulse * 0.16);
          ctx.lineWidth = 1.1;
          ctx.beginPath();
          ctx.arc(output.x, output.y, 13 + localPulse * 5, 0, Math.PI * 2);
          ctx.stroke();
        });
      };

      const drawSourceStream = (time) => {
        const source = screenPoint(sourceNode);
        for (let i = 0; i < 20; i += 1) {
          const y = ((time * 0.04 + i * 56) % (height + 80)) - 40;
          const x = source.x + Math.sin(i * 1.5 + time * 0.0018) * 5;
          const alpha = 0.08 + (i % 4) * 0.03;
          ctx.fillStyle = toRgba(palette.source, alpha);
          ctx.beginPath();
          ctx.arc(x, y, 1.5 + (i % 3) * 0.3, 0, Math.PI * 2);
          ctx.fill();
        }
      };

      const drawParticles = () => {
        const source = screenPoint(sourceNode);

        particles.forEach((particle) => {
          const kb = screenPoint(kbNodes[particle.kbIndex]);
          const output = screenPoint(outputNodes[particle.outIndex]);
          const firstCurve = buildCurve(source, kb, particle.kbIndex % 2 === 0 ? -0.14 : 0.14);
          const direction = output.y < kb.y ? -1 : output.y > kb.y ? 1 : 0;
          const secondCurve = buildCurve(kb, output, direction * (0.11 + particle.kbIndex * 0.012));
          const curve = particle.phase === 0 ? firstCurve : secondCurve;
          const point = pointOnCurve(curve, Math.max(0, Math.min(1, particle.t)));
          const jitterX = Math.sin(particle.wobble + particle.t * 6.4) * 1.7;
          const jitterY = Math.cos(particle.wobble + particle.t * 5.6) * 1.2;
          const color = particle.phase === 0 ? palette.particleSoft : palette.particle;

          ctx.fillStyle = toRgba(color, particle.alpha);
          ctx.beginPath();
          ctx.arc(point.x + jitterX, point.y + jitterY, particle.size, 0, Math.PI * 2);
          ctx.fill();
        });

        ripples.forEach((ripple) => {
          const progress = Math.min(1, ripple.life / ripple.ttl);
          const radius = ripple.r + progress * (ripple.type === "output" ? 11 : 8);
          const color = ripple.type === "output" ? palette.output : palette.kb;
          ctx.strokeStyle = toRgba(color, ripple.alpha * (1 - progress));
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.arc(ripple.x, ripple.y, radius, 0, Math.PI * 2);
          ctx.stroke();
        });
      };

      const updateState = (dt) => {
        spawnTimer += dt;
        while (spawnTimer >= 85) {
          if (particles.length < 120) {
            spawnParticle();
          }
          spawnTimer -= 85;
        }

        particles = particles.filter((particle) => {
          particle.t += particle.speed * dt / 1000;
          if (particle.phase === 0 && particle.t >= 1) {
            const kb = screenPoint(kbNodes[particle.kbIndex]);
            spawnRipple(kb.x, kb.y, "kb");
            particle.phase = 1;
            particle.t = 0;
            return true;
          }
          if (particle.phase === 1 && particle.t >= 1) {
            const output = screenPoint(outputNodes[particle.outIndex]);
            spawnRipple(output.x, output.y, "output");
            return false;
          }
          return true;
        });

        ripples = ripples.filter((ripple) => {
          ripple.life += dt;
          return ripple.life <= ripple.ttl;
        });
      };

      const drawFrame = (time) => {
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawSourceStream(time);
        drawRoutes(time);
        drawNodes(time);
        drawParticles();
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
      };

      const seedParticles = () => {
        particles = [];
        ripples = [];
        for (let i = 0; i < 26; i += 1) {
          spawnParticle(true);
        }
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }

        updatePalette();
        resize();
        seedParticles();
        spawnTimer = 0;
        lastFrame = 0;
        drawFrame(0);

        if (prefersReducedMotion.matches) {
          return;
        }

        const loop = (timestamp) => {
          const dt = lastFrame ? Math.min(34, timestamp - lastFrame) : 16;
          lastFrame = timestamp;
          updateState(dt);
          drawFrame(timestamp);
          animationId = window.requestAnimationFrame(loop);
        };
        animationId = window.requestAnimationFrame(loop);
      };

      start();

      window.addEventListener("resize", () => {
        resize();
        drawFrame(performance.now());
      }, { passive: true });

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
        drawFrame(performance.now());
      });

      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });
    })();
  </script>
</div>
