---
title: "AI-Augmented Search for Systematic Reviews: A Comparative Analysis"
collection: publications
category: conferences
permalink: /publication/2025-asist-ai-augmented-search
excerpt: 'A comparative analysis of AI-augmented search methods for systematic reviews published in ASIS&T proceedings.'
date: 2025-01-10
venue: 'Proceedings of the Association for Information Science and Technology (ASIS&T)'
citation: 'Valerie Vera*, Vedant Khandelwal*, Kaushik Roy, Ritvik Garimella, Harshul Surana, and Amit Sheth. (2025). &quot;AI-Augmented Search for Systematic Reviews: A Comparative Analysis.&quot; <i>Proceedings of the Association for Information Science and Technology</i> 62, no. 1: 705-717. (* Equal contribution)'
paperurl: https://dl.acm.org/doi/10.1002/pra2.1290
header:
  teaser: /images/publications/ai-augmented-search/figure1-architecture.png
---

<div class="paper-ai-augmented-search">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="review-network" role="presentation"></canvas>
  </div>
  <div class="paper-content">
    <p class="paper-lede">This paper provides a comparative analysis of AI-augmented search methods for systematic reviews, with a focus on relevance, reproducibility, and interpretability.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#paper-citation">Citation</a>
      <a class="paper-jump-link" href="#paper-why">Why</a>
      <a class="paper-jump-link" href="#paper-what">What</a>
      <a class="paper-jump-link" href="#paper-how">How</a>
      <a class="paper-jump-link" href="#paper-key">Key contributions</a>
    </nav>

    <section id="paper-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Systematic reviews are slow and labor-intensive (reported average 67 weeks), and search strategy errors can undermine what evidence gets included.</li>
        <li>This paper focuses on the searching stage, where AI-generated strategies can be hard to reproduce or inspect, making it risky to rely on them without expert oversight.</li>
      </ul>
    </section>

    <section id="paper-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>We compared a human-in-the-loop neurosymbolic system (NeuroLit Navigator) against three commercial LLM-based tools (Scite, Consensus, Perplexity) for systematic-review-style searching.</li>
        <li>Across public health and computer science queries, we evaluated outputs for relevancy, reproducibility, interpretability, and controlled vocabulary usage.</li>
        <li>With iterative refinement enabled, NeuroLit Navigator reached a mean relevance of 65% on computer science queries while remaining reproducible and interpretable.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table 3: Computer science comparison across systems">
          <table class="paper-table">
            <thead>
              <tr>
                <th>System</th>
                <th>Relevance %</th>
                <th>Reproducibility</th>
                <th>Interpretability</th>
                <th>Use of Controlled Vocabulary</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Scite</td>
                <td>38%</td>
                <td>No</td>
                <td>No</td>
                <td>No</td>
              </tr>
              <tr>
                <td>Consensus</td>
                <td>47%</td>
                <td>No</td>
                <td>No</td>
                <td>No</td>
              </tr>
              <tr>
                <td>Perplexity</td>
                <td>40%</td>
                <td>No</td>
                <td>No</td>
                <td>No</td>
              </tr>
              <tr>
                <td>NeuroLit Navigator</td>
                <td>65%</td>
                <td>Yes</td>
                <td>Yes</td>
                <td>Yes</td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table 1. NeuroLit Navigator is the only system reporting reproducible, interpretable Boolean queries while achieving higher relevance in the computer science domain.</figcaption>
      </figure>

      <p class="paper-reference">In the evaluation, NeuroLit Navigator is the only tool that supports reproducible and interpretable query logic (Table 1).</p>
    </section>

    <section id="paper-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li>Take a research question plus 1–2 exemplar (“gold standard”) articles from the librarian.</li>
        <li>Extract key entities via domain NER (e.g., SciSpacy).</li>
        <li>Expand terms using MeSH/UMLS (graph-based hops) and a domain LLM (e.g., ClinicalBERT) for related phrasing.</li>
        <li>Build a Boolean query, then retrieve from PubMed (Entrez API) and re-rank via embeddings (e.g., MPNet) with similarity scores shown to users.</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/ai-augmented-search/figure1-architecture.png" alt="NeuroLit Navigator three-stage pipeline: entity extraction, query expansion, and retrieval with re-ranking.">
        <figcaption>Figure 1. Three-stage workflow from librarian inputs to Boolean query construction and PubMed retrieval with re-ranking.</figcaption>
      </figure>

      <p class="paper-reference">The system is organized as a three-stage pipeline from entity extraction to query expansion to retrieval and re-ranking (Figure 1).</p>
    </section>

    <section id="paper-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>An empirical comparison of NeuroLit Navigator vs. Scite/Consensus/Perplexity on systematic-review-oriented criteria (not only relevance).</li>
        <li>Evidence that human-in-the-loop, structured vocabulary integration supports reproducibility and interpretability that commercial systems did not expose.</li>
        <li>A staged neurosymbolic pipeline that explicitly combines controlled vocabularies (MeSH/UMLS) with neural components for query expansion and re-ranking.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-ai-augmented-search {
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
      --paper-accent-soft: var(--global-link-color-hover);
      --paper-table-header: var(--global-thead-color);
      --paper-table-even: rgba(0, 0, 0, 0.04);
      --paper-table-border: var(--global-border-color);
    }

    html[data-theme="dark"] .paper-ai-augmented-search {
      --paper-table-header: var(--global-border-color);
      --paper-table-even: rgba(255, 255, 255, 0.06);
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.35);
    }

    .paper-ai-augmented-search .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-ai-augmented-search .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
    }

    .paper-ai-augmented-search .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-ai-augmented-search .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-ai-augmented-search .paper-note {
      margin-top: 0;
      color: var(--paper-ink-soft);
    }

    .paper-ai-augmented-search .paper-jump-links {
      display: flex;
      gap: 0.5rem;
      margin: 0.75rem 0 0.2rem;
      position: fixed;
      left: 50%;
      bottom: calc(12px + env(safe-area-inset-bottom));
      transform: translateX(-50%);
      width: min(980px, calc(100vw - 1.4rem));
      flex-wrap: nowrap;
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
      overscroll-behavior-x: contain;
      padding: 0.5rem;
      border: 1px solid var(--paper-border);
      border-radius: 999px;
      background: color-mix(in srgb, var(--paper-panel) 78%, transparent);
      box-shadow: 0 8px 22px rgba(0, 0, 0, 0.16);
      backdrop-filter: blur(10px);
      z-index: 30;
      scrollbar-width: none;
    }

    .paper-ai-augmented-search .paper-jump-links::-webkit-scrollbar {
      display: none;
    }

    .paper-ai-augmented-search .paper-jump-link {
      display: inline-block;
      border: 1px solid var(--paper-border);
      border-radius: 999px;
      background: var(--paper-panel);
      color: var(--paper-ink);
      padding: 0.35rem 0.75rem;
      font-size: 0.88rem;
      line-height: 1.2;
      text-decoration: none;
      transition: border-color 0.2s ease, color 0.2s ease, background-color 0.2s ease;
      white-space: nowrap;
      flex: 0 0 auto;
    }

    .paper-ai-augmented-search .paper-jump-link:hover,
    .paper-ai-augmented-search .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-ai-augmented-search .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-ai-augmented-search .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: var(--paper-panel-soft);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    .paper-ai-augmented-search .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink-strong);
    }

    .paper-ai-augmented-search .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), var(--paper-accent-soft));
    }

    .paper-ai-augmented-search .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-ai-augmented-search .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: var(--paper-panel);
    }

    .paper-ai-augmented-search .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-ai-augmented-search .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-ai-augmented-search .paper-table-wrap + figcaption {
      color: var(--paper-ink);
    }

    .paper-ai-augmented-search .paper-table-wrap {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .paper-ai-augmented-search .paper-table {
      width: 100%;
      min-width: 560px;
      border-collapse: collapse;
      font-size: 0.95rem;
    }

    .paper-ai-augmented-search .paper-table th,
    .paper-ai-augmented-search .paper-table td {
      border: 1px solid var(--paper-table-border);
      padding: 0.6rem 0.75rem;
      text-align: left;
    }

    .paper-ai-augmented-search .paper-table thead th {
      background: var(--global-link-color);
      color: var(--global-bg-color);
      font-weight: 700;
      border-bottom: 2px solid var(--paper-table-border);
    }

    .paper-ai-augmented-search .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-ai-augmented-search .paper-reference {
      margin-top: 0;
      color: var(--paper-ink-strong);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-ai-augmented-search .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-ai-augmented-search .paper-jump-links {
        width: calc(100vw - 0.8rem);
        bottom: calc(8px + env(safe-area-inset-bottom));
        border-radius: 14px;
        padding: 0.42rem;
        gap: 0.42rem;
      }

      .paper-ai-augmented-search .paper-jump-link {
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-ai-augmented-search .paper-section {
        padding: 1.2rem 1.1rem;
      }

      .paper-ai-augmented-search .paper-table {
        font-size: 0.9rem;
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

      const canvas = document.getElementById("review-network");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d");
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");
      const anchors = [0.03, 0.1, 0.35, 0.6, 0.85, 0.96];
      const stageFractions = [0.1, 0.35, 0.6, 0.85];
      const topRatios = [0.26, 0.28, 0.32, 0.38, 0.44, 0.47];
      const bottomRatios = [0.74, 0.72, 0.68, 0.62, 0.56, 0.53];
      const stageDropRates = [0.2, 0.3, 0.22];

      let width = 0;
      let height = 0;
      let papers = [];
      let staticPapers = [];
      let gradient = null;
      let animationId = null;
      let lastSpawnAt = 0;
      let palette = null;

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

      const toRgba = (rgb, alpha) => `rgba(${rgb[0]}, ${rgb[1]}, ${rgb[2]}, ${alpha})`;

      const mixColor = (base, accent, amount) =>
        base.map((channel, index) => Math.round(channel + (accent[index] - channel) * amount));

      const lerp = (start, end, t) => start + (end - start) * t;

      const interpolateByAnchors = (values, xRatio) => {
        if (xRatio <= anchors[0]) {
          return values[0];
        }
        for (let i = 1; i < anchors.length; i += 1) {
          if (xRatio <= anchors[i]) {
            const t = (xRatio - anchors[i - 1]) / (anchors[i] - anchors[i - 1]);
            return lerp(values[i - 1], values[i], t);
          }
        }
        return values[values.length - 1];
      };

      const topAt = (xRatio) => height * interpolateByAnchors(topRatios, xRatio);
      const bottomAt = (xRatio) => height * interpolateByAnchors(bottomRatios, xRatio);

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bgValue = styles.getPropertyValue("--global-bg-color");
        const accentValue = styles.getPropertyValue("--global-link-color");
        const textValue = styles.getPropertyValue("--global-text-color");
        const bgColor = parseColor(bgValue) || [238, 238, 238];
        const accentColor = parseColor(accentValue) || [57, 62, 70];
        const textColor = parseColor(textValue) || [45, 45, 45];
        const start = mixColor(bgColor, accentColor, 0.05);
        const end = mixColor(bgColor, accentColor, 0.11);
        palette = {
          laneFill: mixColor(bgColor, accentColor, 0.16),
          laneStroke: mixColor(bgColor, accentColor, 0.28),
          stageDot: mixColor(bgColor, accentColor, 0.4),
          paperColor: mixColor(bgColor, accentColor, 0.55),
          paperEdge: mixColor(bgColor, textColor, 0.35),
          excludedColor: mixColor(bgColor, textColor, 0.35),
          excludedEdge: mixColor(bgColor, textColor, 0.55),
          start,
          end
        };
        gradient = ctx.createLinearGradient(0, 0, width, height);
        gradient.addColorStop(0, toRgba(start, 0.95));
        gradient.addColorStop(1, toRgba(end, 0.95));
      };

      const createPaper = (xRatio = anchors[0], isStatic = false) => {
        const top = topAt(xRatio);
        const bottom = bottomAt(xRatio);
        const laneSpan = bottom - top;
        return {
          x: width * xRatio,
          y: top + laneSpan * (0.25 + Math.random() * 0.5),
          vx: 0.55 + Math.random() * 0.4,
          vy: (Math.random() - 0.5) * 0.14,
          wobble: Math.random() * Math.PI * 2,
          size: 4 + Math.random() * 2,
          alpha: 0.2 + Math.random() * 0.18,
          stage: 0,
          active: !isStatic || xRatio < 0.78 || Math.random() > 0.45
        };
      };

      const refreshStaticPapers = () => {
        staticPapers = Array.from({ length: 22 }, (_, index) => {
          const t = index / 21;
          const ratio = lerp(anchors[0] + 0.01, anchors[anchors.length - 1] - 0.01, t);
          return createPaper(ratio, true);
        });
      };

      const drawChannel = () => {
        if (!palette) {
          return;
        }

        ctx.beginPath();
        ctx.moveTo(width * anchors[0], topAt(anchors[0]));
        for (let i = 1; i < anchors.length; i += 1) {
          ctx.lineTo(width * anchors[i], topAt(anchors[i]));
        }
        for (let i = anchors.length - 1; i >= 0; i -= 1) {
          ctx.lineTo(width * anchors[i], bottomAt(anchors[i]));
        }
        ctx.closePath();
        ctx.fillStyle = toRgba(palette.laneFill, 0.16);
        ctx.fill();

        ctx.strokeStyle = toRgba(palette.laneStroke, 0.3);
        ctx.lineWidth = 1.5;
        ctx.beginPath();
        ctx.moveTo(width * anchors[0], topAt(anchors[0]));
        for (let i = 1; i < anchors.length; i += 1) {
          ctx.lineTo(width * anchors[i], topAt(anchors[i]));
        }
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(width * anchors[0], bottomAt(anchors[0]));
        for (let i = 1; i < anchors.length; i += 1) {
          ctx.lineTo(width * anchors[i], bottomAt(anchors[i]));
        }
        ctx.stroke();

        stageFractions.forEach((ratio) => {
          const stageX = width * ratio;
          const top = topAt(ratio);
          const bottom = bottomAt(ratio);
          const centerY = (top + bottom) / 2;
          ctx.strokeStyle = toRgba(palette.stageDot, 0.18);
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.moveTo(stageX, top - 20);
          ctx.lineTo(stageX, bottom + 20);
          ctx.stroke();

          ctx.fillStyle = toRgba(palette.stageDot, 0.24);
          ctx.beginPath();
          ctx.arc(stageX, centerY, 3, 0, Math.PI * 2);
          ctx.fill();
        });
      };

      const drawPaper = (paper) => {
        if (!palette || paper.alpha <= 0) {
          return;
        }
        const widthBox = paper.size * 1.45;
        const heightBox = paper.size;
        const fillColor = paper.active ? palette.paperColor : palette.excludedColor;
        const edgeColor = paper.active ? palette.paperEdge : palette.excludedEdge;
        ctx.fillStyle = toRgba(fillColor, paper.alpha);
        ctx.fillRect(
          paper.x - widthBox / 2,
          paper.y - heightBox / 2,
          widthBox,
          heightBox
        );
        ctx.fillStyle = toRgba(edgeColor, paper.alpha * 0.8);
        ctx.fillRect(
          paper.x + widthBox * 0.05,
          paper.y - heightBox / 2,
          widthBox * 0.32,
          heightBox * 0.25
        );
      };

      const drawFrame = (currentPapers) => {
        ctx.clearRect(0, 0, width, height);
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, width, height);
        drawChannel();
        currentPapers.forEach(drawPaper);
      };

      const updatePaper = (paper) => {
        if (paper.active) {
          paper.x += paper.vx;
          paper.wobble += 0.02;
          const xRatio = Math.max(
            anchors[0],
            Math.min(anchors[anchors.length - 1], paper.x / width)
          );
          const top = topAt(xRatio) + 2;
          const bottom = bottomAt(xRatio) - 2;
          const center = (top + bottom) / 2;

          paper.y += paper.vy + Math.sin(paper.wobble) * 0.07;
          paper.y += (center - paper.y) * 0.03;
          if (paper.y < top) {
            paper.y = top;
            paper.vy = Math.abs(paper.vy) * 0.6;
          }
          if (paper.y > bottom) {
            paper.y = bottom;
            paper.vy = -Math.abs(paper.vy) * 0.6;
          }

          while (
            paper.stage < stageFractions.length - 1 &&
            xRatio >= stageFractions[paper.stage + 1]
          ) {
            if (Math.random() < stageDropRates[paper.stage]) {
              paper.active = false;
              paper.vx *= 0.24;
              paper.vy = 0.35 + Math.random() * 0.35;
              break;
            }
            paper.stage += 1;
          }

          if (paper.x > width * anchors[anchors.length - 1]) {
            paper.alpha -= 0.015;
          }
        } else {
          paper.x += paper.vx;
          paper.y += paper.vy;
          paper.vy += 0.015;
          paper.alpha -= 0.012;
        }

        return (
          paper.alpha > 0.02 &&
          paper.x < width + 24 &&
          paper.y < height + 32
        );
      };

      const tick = (timestamp) => {
        if (prefersReducedMotion.matches) {
          drawFrame(staticPapers);
          return;
        }

        if (!lastSpawnAt) {
          lastSpawnAt = timestamp;
        }

        const spawnInterval = 120;
        while (timestamp - lastSpawnAt >= spawnInterval) {
          if (papers.length < 96) {
            papers.push(createPaper());
          }
          lastSpawnAt += spawnInterval;
        }

        papers = papers.filter(updatePaper);
        drawFrame(papers);
        animationId = window.requestAnimationFrame(tick);
      };

      const resize = () => {
        width = window.innerWidth;
        height = window.innerHeight;
        const dpr = Math.min(window.devicePixelRatio || 1, 2);
        canvas.width = width * dpr;
        canvas.height = height * dpr;
        canvas.style.width = `${width}px`;
        canvas.style.height = `${height}px`;
        ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
        updatePalette();
        refreshStaticPapers();
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }

        lastSpawnAt = 0;
        if (prefersReducedMotion.matches) {
          drawFrame(staticPapers);
          return;
        }

        papers = Array.from({ length: 24 }, () =>
          createPaper(anchors[0] + Math.random() * 0.28)
        );
        animationId = window.requestAnimationFrame(tick);
      };

      resize();
      start();

      window.addEventListener("resize", () => {
        resize();
        start();
      });

      const handleMotionChange = () => {
        resize();
        start();
      };

      if (prefersReducedMotion.addEventListener) {
        prefersReducedMotion.addEventListener("change", handleMotionChange);
      } else if (prefersReducedMotion.addListener) {
        prefersReducedMotion.addListener(handleMotionChange);
      }

      const observer = new MutationObserver(() => {
        updatePalette();
        drawFrame(prefersReducedMotion.matches ? staticPapers : papers);
      });

      observer.observe(root, { attributes: true, attributeFilter: ["data-theme"] });
    })();
  </script>
</div>
