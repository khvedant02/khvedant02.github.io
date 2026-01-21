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
---

<div class="paper-ai-augmented-search">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="review-network" role="presentation"></canvas>
  </div>
  <div class="paper-content">
    <p class="paper-lede">This paper provides a comparative analysis of AI-augmented search methods for systematic reviews, with a focus on relevance, reproducibility, and interpretability.</p>

    <section class="paper-section">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Systematic reviews are slow and labor-intensive (reported average 67 weeks), and search strategy errors can undermine what evidence gets included.</li>
        <li>This paper focuses on the searching stage, where AI-generated strategies can be hard to reproduce or inspect, making it risky to rely on them without expert oversight.</li>
      </ul>
    </section>

    <section class="paper-section">
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
        <figcaption>Table 3. NeuroLit Navigator is the only system reporting reproducible, interpretable Boolean queries while achieving higher relevance in the computer science setting.</figcaption>
      </figure>

      <p class="paper-reference">In the computer science evaluation, NeuroLit Navigator is the only tool that supports reproducible and interpretable query logic (Table 3).</p>
    </section>

    <section class="paper-section">
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

    <section class="paper-section">
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
      color: var(--global-text-color-light);
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
      const canvas = document.getElementById("review-network");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d");
      if (!ctx) {
        return;
      }

      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");
      const root = document.documentElement;
      let width = 0;
      let height = 0;
      let nodes = [];
      let gradient = null;
      let animationId = null;
      let pulseId = null;
      let pulses = [];
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

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bgValue = styles.getPropertyValue("--global-bg-color");
        const accentValue = styles.getPropertyValue("--global-link-color");
        const bgColor = parseColor(bgValue) || [238, 238, 238];
        const accentColor = parseColor(accentValue) || [57, 62, 70];
        const start = mixColor(bgColor, accentColor, 0.06);
        const end = mixColor(bgColor, accentColor, 0.12);
        palette = { bgColor, accentColor, start, end };
        gradient = ctx.createLinearGradient(0, 0, width, height);
        gradient.addColorStop(0, toRgba(start, 0.96));
        gradient.addColorStop(1, toRgba(end, 0.96));
      };

      const createNodes = () => {
        const baseCount = Math.max(28, Math.min(56, Math.round(Math.sqrt(width * height) / 18)));
        nodes = Array.from({ length: baseCount }, (_, index) => {
          const angle = Math.random() * Math.PI * 2;
          const speed = 0.18 + Math.random() * 0.35;
          return {
            x: Math.random() * width,
            y: Math.random() * height,
            vx: Math.cos(angle) * speed,
            vy: Math.sin(angle) * speed,
            size: 1.1 + Math.random() * 1.9
          };
        });
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
        createNodes();
        drawFrame();
      };

      const drawConnections = () => {
        const maxDistance = 150;
        if (!palette) {
          return;
        }
        for (let i = 0; i < nodes.length; i += 1) {
          for (let j = i + 1; j < nodes.length; j += 1) {
            const dx = nodes[i].x - nodes[j].x;
            const dy = nodes[i].y - nodes[j].y;
            const dist = Math.hypot(dx, dy);
            if (dist < maxDistance) {
              const opacity = 1 - dist / maxDistance;
              ctx.strokeStyle = toRgba(palette.accentColor, 0.14 * opacity);
              ctx.lineWidth = 1;
              ctx.beginPath();
              ctx.moveTo(nodes[i].x, nodes[i].y);
              ctx.lineTo(nodes[j].x, nodes[j].y);
              ctx.stroke();
            }
          }
        }
      };

      const drawPulses = () => {
        if (!palette) {
          return;
        }
        pulses = pulses.filter((pulse) => pulse.radius < pulse.maxRadius);
        pulses.forEach((pulse) => {
          const alpha = Math.max(0, 1 - pulse.radius / pulse.maxRadius);
          ctx.strokeStyle = toRgba(palette.accentColor, 0.22 * alpha);
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.arc(pulse.x, pulse.y, pulse.radius, 0, Math.PI * 2);
          ctx.stroke();
          pulse.radius += pulse.speed;
        });
      };

      const drawNodes = () => {
        if (!palette) {
          return;
        }
        nodes.forEach((node) => {
          ctx.fillStyle = toRgba(palette.accentColor, 0.22);
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.size, 0, Math.PI * 2);
          ctx.fill();
        });
      };

      const drawFrame = () => {
        ctx.clearRect(0, 0, width, height);
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, width, height);
        drawConnections();
        drawPulses();
        drawNodes();
      };

      const step = () => {
        nodes.forEach((node) => {
          node.x += node.vx;
          node.y += node.vy;
          if (node.x < 0 || node.x > width) {
            node.vx *= -1;
          }
          if (node.y < 0 || node.y > height) {
            node.vy *= -1;
          }
        });
        drawFrame();
        animationId = window.requestAnimationFrame(step);
      };

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }
        if (pulseId) {
          window.clearInterval(pulseId);
          pulseId = null;
        }
        if (prefersReducedMotion.matches) {
          canvas.style.display = "none";
          drawFrame();
          return;
        }
        canvas.style.display = "block";
        pulseId = window.setInterval(() => {
          const source = nodes[Math.floor(Math.random() * nodes.length)];
          if (!source) {
            return;
          }
          pulses.push({
            x: source.x,
            y: source.y,
            radius: 0,
            maxRadius: 160 + Math.random() * 120,
            speed: 1.4 + Math.random() * 0.8
          });
        }, 1100);
        animationId = window.requestAnimationFrame(step);
      };

      resize();
      start();

      window.addEventListener("resize", () => {
        resize();
        start();
      });

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
