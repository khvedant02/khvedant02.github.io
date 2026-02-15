---
title: "NeuroLit Navigator: A Neurosymbolic Approach to Scholarly Article Searches for Systematic Reviews"
collection: publications
category: preprints
permalink: /publication/2025-arxiv-neurolit-navigator
excerpt: "A neurosymbolic retrieval pipeline for faster, reproducible first-iteration search in systematic reviews."
date: 2025-03-01
venue: 'arXiv preprint arXiv:2503.00278'
paperurl: 'https://arxiv.org/abs/2503.00278'
citation: 'Vedant Khandelwal, Kaushik Roy, Valerie Lookingbill, Ritvik Garimella, Harshul Surana, Heather Heckman, and Amit Sheth. (2025). &quot;NeuroLit Navigator: A Neurosymbolic Approach to Scholarly Article Searches for Systematic Reviews.&quot; <i>arXiv preprint arXiv:2503.00278</i>.'
header:
  teaser: /images/publications/neurolit/figure1-architecture.png
---
<div class="paper-neurolit">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="neurolit-flow" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper presents NeuroLit Navigator, a neurosymbolic workflow that supports faster and more reproducible first-iteration article retrieval for systematic reviews.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#neurolit-why">Why</a>
      <a class="paper-jump-link" href="#neurolit-what">What</a>
      <a class="paper-jump-link" href="#neurolit-how">How</a>
      <a class="paper-jump-link" href="#neurolit-key">Key contributions</a>
    </nav>

    <section id="neurolit-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Systematic review query development averages 8-15 hours, so the first search iteration is labor-intensive.</li>
        <li>Systematic review publications are growing at 26% per year, increasing demand for scalable and reproducible search workflows.</li>
        <li>General LLM tools struggle with domain-specific vocabulary, controlled terminology, and citation reliability.</li>
        <li>Keyword-based and LLM-only retrieval systems often trade precision for recall (or vice versa) and often lack reproducibility.</li>
        <li>The first iteration of article retrieval strongly influences downstream screening effort and overall systematic review quality.</li>
      </ul>
    </section>

    <section id="neurolit-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Introduced <strong>NeuroLit Navigator</strong>, a neurosymbolic system combining domain-specific LLMs with biomedical knowledge graphs (MeSH, UMLS).</li>
        <li>Used named entity recognition, knowledge graph expansion (up to two hops), and ClinicalBERT-based query expansion.</li>
        <li>Applied semantic re-ranking with MPNet embeddings, which achieved <strong>36% relevance</strong>, the highest among tested embedding choices.</li>
        <li>Retrieved and presented the top <strong>k = 5</strong> articles for structured librarian feedback.</li>
        <li>Demonstrated a <strong>90% reduction in initial search time</strong> while supporting controlled vocabulary, interpretability, and reproducibility.</li>
      </ul>
    </section>

    <section id="neurolit-how" class="paper-section paper-anchor">
      <h2>How it works</h2>
      <ul class="paper-list">
        <li><strong>User input + sentinel article:</strong> extract key biomedical entities via SciSpacy NER.</li>
        <li><strong>Vocabulary extension:</strong> expand entities using MeSH/UMLS terms within two hops, filtered by semantic similarity.</li>
        <li><strong>Query expansion:</strong> mask and substitute terms using ClinicalBERT to generate related variants.</li>
        <li><strong>Iterative query refinement:</strong> start specific and progressively relax constraints until a minimum result set is retrieved.</li>
        <li><strong>Retrieval + re-ranking:</strong> query PubMed via Entrez API and re-rank with MPNet embeddings, then return top <strong>k = 5</strong> articles for librarian review.</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/neurolit/figure1-architecture.png" alt="Three-step neurosymbolic NeuroLit Navigator pipeline with NER, knowledge-graph vocabulary expansion, query expansion, and semantic re-ranking.">
        <figcaption>Figure 1. Three-step neurosymbolic pipeline combining NER, KG-based vocabulary extension, LLM query expansion, and semantic re-ranking.</figcaption>
      </figure>

      <p class="paper-reference">The full neurosymbolic pipeline is illustrated in Figure 1.</p>
    </section>

    <section id="neurolit-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>A <strong>neurosymbolic SR retrieval pipeline</strong> integrating controlled vocabulary and LLM-based expansion.</li>
        <li>A <strong>zero-shot query formulation approach</strong> that eliminates manual setup for first-iteration searches.</li>
        <li>Empirical comparison of biomedical embedding models showing <strong>36% relevance with MPNet</strong>.</li>
        <li>Demonstrated <strong>90% reduction in initial search time</strong> in librarian-facing deployment.</li>
        <li>Comparative evaluation showing NeuroLit Navigator uniquely combines relevance, reproducibility, interpretability, and controlled vocabulary support.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table 1: System comparison across relevance, reproducibility, interpretability, and controlled vocabulary">
          <table class="paper-table">
            <thead>
              <tr>
                <th>System</th>
                <th>Relevance %</th>
                <th>R</th>
                <th>I</th>
                <th>CV</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Scite</td>
                <td>33%</td>
                <td>No</td>
                <td>No</td>
                <td>No</td>
              </tr>
              <tr>
                <td>Consensus</td>
                <td>38%</td>
                <td>No</td>
                <td>No</td>
                <td>No</td>
              </tr>
              <tr>
                <td>Perplexity</td>
                <td>33%</td>
                <td>No</td>
                <td>No</td>
                <td>No</td>
              </tr>
              <tr>
                <td>GEAR-Up</td>
                <td>26.6%</td>
                <td>No</td>
                <td>Yes</td>
                <td>No</td>
              </tr>
              <tr>
                <td><strong>NeuroLit Navigator</strong></td>
                <td><strong>36%</strong></td>
                <td><strong>Yes</strong></td>
                <td><strong>Yes</strong></td>
                <td><strong>Yes</strong></td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table 1. Comparison of relevance %, reproducibility (R), interpretability (I), and controlled vocabulary (CV) across SR tools.</figcaption>
      </figure>

      <p class="paper-reference">As shown in Table 1, the system uniquely combines reproducibility and controlled vocabulary with competitive relevance.</p>
    </section>
  </div>

  <style>
    .paper-neurolit {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-ink-strong: var(--global-text-color);
      --paper-panel: var(--global-bg-color);
      --paper-border: var(--global-border-color);
      --paper-shadow: 0 14px 30px rgba(0, 0, 0, 0.12);
      --paper-accent: var(--global-link-color);
      --paper-accent-soft: var(--global-link-color-hover);
      --paper-table-even: rgba(0, 0, 0, 0.04);
      --paper-table-border: var(--global-border-color);
    }

    html[data-theme="dark"] .paper-neurolit {
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.35);
      --paper-table-even: rgba(255, 255, 255, 0.06);
    }

    .paper-neurolit .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-neurolit .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.35;
    }

    .paper-neurolit .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-neurolit .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-neurolit .paper-jump-links {
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

    .paper-neurolit .paper-jump-link {
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

    .paper-neurolit .paper-jump-link:hover,
    .paper-neurolit .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-neurolit .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-neurolit .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-neurolit .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-neurolit .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink-strong);
    }

    .paper-neurolit .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), var(--paper-accent-soft));
    }

    .paper-neurolit .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-neurolit .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-neurolit .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-neurolit .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-neurolit .paper-table-wrap {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .paper-neurolit .paper-table {
      width: 100%;
      min-width: 560px;
      border-collapse: collapse;
      font-size: 0.95rem;
    }

    .paper-neurolit .paper-table th,
    .paper-neurolit .paper-table td {
      border: 1px solid var(--paper-table-border);
      padding: 0.6rem 0.75rem;
      text-align: left;
    }

    .paper-neurolit .paper-table thead th {
      background: var(--global-link-color);
      color: var(--global-bg-color);
      font-weight: 700;
      border-bottom: 2px solid var(--paper-table-border);
    }

    .paper-neurolit .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-neurolit .paper-reference {
      margin-top: 0;
      color: var(--paper-ink-strong);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-neurolit .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-neurolit .paper-jump-links {
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

      .paper-neurolit .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-neurolit .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-neurolit .paper-section {
        padding: 1.2rem 1.1rem;
      }

      .paper-neurolit .paper-table {
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

      const canvas = document.getElementById("neurolit-flow");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");
      const stageKeys = ["input", "ner", "kg", "query", "rank", "topk"];
      const stageLabels = ["Input", "NER", "KG", "LLM", "Rank", "k=5"];
      const stageY = [0.43, 0.34, 0.5, 0.34, 0.5, 0.43];
      const passes = [0.82, 0.88, 0.84, 0.72, 0.75];

      let width = 0;
      let height = 0;
      let dpr = 1;
      let stagePoints = {};
      let packets = [];
      let sparks = [];
      let animationId = null;
      let lastFrame = 0;
      let spawnTimer = 0;
      let palette = null;

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
      const rand = (min, max) => min + Math.random() * (max - min);

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bg = parseColor(styles.getPropertyValue("--global-bg-color")) || [240, 243, 245];
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [45, 120, 160];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [42, 52, 64];

        palette = {
          wash: mixColor(bg, accent, 0.24),
          edge: mixColor(bg, accent, 0.48),
          edgeSoft: mixColor(bg, accent, 0.3),
          nodeFill: mixColor(bg, accent, 0.16),
          nodeStroke: mixColor(bg, text, 0.34),
          label: mixColor(bg, text, 0.62),
          packet: mixColor(bg, accent, 0.72),
          reject: mixColor(bg, text, 0.58),
          sparkle: mixColor(bg, accent, 0.78)
        };
      };

      const buildLayout = () => {
        stagePoints = {};
        stageKeys.forEach((key, index) => {
          stagePoints[key] = {
            x: width * (0.08 + index * 0.17),
            y: height * stageY[index]
          };
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
        buildLayout();
      };

      const spawnPacket = (seeded = false) => {
        const start = stagePoints.input;
        packets.push({
          stage: 0,
          progress: seeded ? rand(0, 0.95) : 0,
          x: start.x,
          y: start.y + rand(-6, 6),
          speed: rand(0.22, 0.36),
          radius: rand(1.6, 2.8),
          alive: true,
          accepted: true,
          alpha: rand(0.22, 0.4)
        });
      };

      const spawnSpark = (x, y, rejected = false) => {
        const count = rejected ? 6 : 4;
        for (let i = 0; i < count; i += 1) {
          sparks.push({
            x,
            y,
            vx: rand(-0.35, 0.35),
            vy: rejected ? rand(-0.12, 0.2) : rand(-0.25, 0.15),
            life: rand(340, 620),
            t: 0,
            size: rand(0.9, 1.9),
            rejected
          });
        }
      };

      const seed = () => {
        packets = [];
        sparks = [];
        for (let i = 0; i < 22; i += 1) {
          spawnPacket(true);
        }
      };

      const lerp = (a, b, t) => a + (b - a) * t;

      const drawEdge = (from, to, isMain) => {
        ctx.strokeStyle = toRgba(isMain ? palette.edge : palette.edgeSoft, isMain ? 0.34 : 0.24);
        ctx.lineWidth = isMain ? 1.7 : 1.2;
        ctx.beginPath();
        ctx.moveTo(from.x, from.y);
        ctx.lineTo(to.x, to.y);
        ctx.stroke();

        const angle = Math.atan2(to.y - from.y, to.x - from.x);
        const size = isMain ? 5 : 4;
        ctx.fillStyle = toRgba(isMain ? palette.edge : palette.edgeSoft, isMain ? 0.36 : 0.26);
        ctx.beginPath();
        ctx.moveTo(to.x, to.y);
        ctx.lineTo(to.x - Math.cos(angle - Math.PI / 7) * size, to.y - Math.sin(angle - Math.PI / 7) * size);
        ctx.lineTo(to.x - Math.cos(angle + Math.PI / 7) * size, to.y - Math.sin(angle + Math.PI / 7) * size);
        ctx.closePath();
        ctx.fill();
      };

      const drawGraph = () => {
        const wash = ctx.createRadialGradient(width * 0.45, height * 0.44, 80, width * 0.45, height * 0.44, Math.max(width, height) * 0.7);
        wash.addColorStop(0, toRgba(palette.wash, 0.1));
        wash.addColorStop(1, "rgba(0,0,0,0)");
        ctx.fillStyle = wash;
        ctx.fillRect(0, 0, width, height);

        for (let i = 0; i < stageKeys.length - 1; i += 1) {
          const from = stagePoints[stageKeys[i]];
          const to = stagePoints[stageKeys[i + 1]];
          drawEdge(from, to, true);
        }

        const kg = stagePoints.kg;
        const upper = { x: kg.x + 28, y: kg.y - 55 };
        const lower = { x: kg.x + 28, y: kg.y + 55 };
        drawEdge(kg, upper, false);
        drawEdge(kg, lower, false);
        drawEdge(upper, stagePoints.query, false);
        drawEdge(lower, stagePoints.query, false);

        stageKeys.forEach((key, index) => {
          const point = stagePoints[key];
          const radius = key === "topk" ? 21 : 18;
          ctx.beginPath();
          ctx.fillStyle = toRgba(palette.nodeFill, key === "topk" ? 0.34 : 0.24);
          ctx.strokeStyle = toRgba(palette.nodeStroke, 0.42);
          ctx.lineWidth = 1.3;
          ctx.arc(point.x, point.y, radius, 0, Math.PI * 2);
          ctx.fill();
          ctx.stroke();

          ctx.fillStyle = toRgba(palette.label, 0.82);
          ctx.font = "600 12px ui-sans-serif, system-ui, -apple-system, Segoe UI, sans-serif";
          ctx.textAlign = "center";
          ctx.textBaseline = "middle";
          ctx.fillText(stageLabels[index], point.x, point.y);
        });
      };

      const updatePackets = (dt) => {
        packets.forEach((packet) => {
          if (!packet.alive) {
            return;
          }

          const current = stagePoints[stageKeys[packet.stage]];
          const next = stagePoints[stageKeys[Math.min(packet.stage + 1, stageKeys.length - 1)]];
          packet.progress += (packet.speed * dt) / 1000;
          const t = Math.min(packet.progress, 1);
          packet.x = lerp(current.x, next.x, t);
          packet.y = lerp(current.y, next.y, t) + Math.sin((packet.stage + t) * Math.PI * 2) * 2.4;

          if (packet.progress < 1) {
            return;
          }

          if (packet.stage >= stageKeys.length - 2) {
            spawnSpark(packet.x, packet.y, false);
            packet.alive = false;
            return;
          }

          const keep = Math.random() <= passes[packet.stage];
          packet.accepted = keep;
          if (!keep) {
            spawnSpark(packet.x, packet.y, true);
            packet.alive = false;
            return;
          }

          packet.stage += 1;
          packet.progress = 0;
          packet.x = stagePoints[stageKeys[packet.stage]].x;
          packet.y = stagePoints[stageKeys[packet.stage]].y;
        });

        packets = packets.filter((packet) => packet.alive);
      };

      const drawPackets = () => {
        packets.forEach((packet) => {
          ctx.beginPath();
          ctx.arc(packet.x, packet.y, packet.radius, 0, Math.PI * 2);
          const color = packet.accepted ? palette.packet : palette.reject;
          ctx.fillStyle = toRgba(color, packet.alpha);
          ctx.fill();
        });
      };

      const updateSparks = (dt) => {
        sparks.forEach((spark) => {
          spark.t += dt;
          spark.x += (spark.vx * dt) / 10;
          spark.y += (spark.vy * dt) / 10;
        });
        sparks = sparks.filter((spark) => spark.t < spark.life);
      };

      const drawSparks = () => {
        sparks.forEach((spark) => {
          const life = 1 - spark.t / spark.life;
          ctx.beginPath();
          ctx.arc(spark.x, spark.y, spark.size * (0.7 + life * 0.7), 0, Math.PI * 2);
          const rgb = spark.rejected ? palette.reject : palette.sparkle;
          ctx.fillStyle = toRgba(rgb, 0.26 * life);
          ctx.fill();
        });
      };

      const render = (timestamp) => {
        if (!lastFrame) {
          lastFrame = timestamp;
        }
        const dt = Math.min(34, timestamp - lastFrame);
        lastFrame = timestamp;

        spawnTimer += dt;
        if (spawnTimer > 210) {
          spawnPacket(false);
          spawnTimer = 0;
        }

        ctx.clearRect(0, 0, width, height);
        drawGraph();
        updatePackets(dt);
        drawPackets();
        updateSparks(dt);
        drawSparks();

        animationId = window.requestAnimationFrame(render);
      };

      const stop = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }
      };

      const drawStatic = () => {
        stop();
        ctx.clearRect(0, 0, width, height);
        drawGraph();
        drawPackets();
        drawSparks();
      };

      const start = () => {
        stop();
        if (prefersReducedMotion.matches) {
          drawStatic();
          return;
        }
        lastFrame = 0;
        spawnTimer = 0;
        animationId = window.requestAnimationFrame(render);
      };

      const rebuild = () => {
        updatePalette();
        resize();
        seed();
        start();
      };

      rebuild();
      window.addEventListener("resize", rebuild);

      if (typeof prefersReducedMotion.addEventListener === "function") {
        prefersReducedMotion.addEventListener("change", start);
      } else if (typeof prefersReducedMotion.addListener === "function") {
        prefersReducedMotion.addListener(start);
      }

      const observer = new MutationObserver((mutations) => {
        if (mutations.some((mutation) => mutation.attributeName === "data-theme")) {
          rebuild();
        }
      });
      observer.observe(root, { attributes: true });
    })();
  </script>
</div>
