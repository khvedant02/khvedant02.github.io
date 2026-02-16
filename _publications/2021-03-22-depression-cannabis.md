---
title: "\"Is depression related to cannabis?\": A knowledge-infused model for entity and relation extraction with limited Supervision"
collection: publications
category: workshops
permalink: /publication/2021-aaai-make-depression-cannabis
excerpt: "A knowledge-infused relation extraction model combining ontology guidance, GPT-3 embeddings, and contrastive learning under limited supervision."
date: 2021-03-22
venue: "AAAI 2021 Spring Symposium on Combining Machine Learning and Knowledge Engineering (AAAI-MAKE)"
paperurl: "https://ceur-ws.org/Vol-2846/paper9.pdf"
citation: 'Kaushik Roy, Usha Lokala, Vedant Khandelwal, and Amit Sheth. (2021). &quot;Is depression related to cannabis?: A knowledge-infused model for entity and relation extraction with limited Supervision.&quot; <i>Proceedings of the AAAI 2021 Spring Symposium on Combining Machine Learning and Knowledge Engineering (AAAI-MAKE 2021)</i>.'
header:
  teaser: /images/publications/depression/figure1.png
---

<div class="paper-depression-relations">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="depression-relation-net" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper studies how to extract structured cannabis-depression relationships from noisy Twitter text when only a small expert-labeled subset is available.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#dep-why">Why</a>
      <a class="paper-jump-link" href="#dep-what">What</a>
      <a class="paper-jump-link" href="#dep-how">How</a>
      <a class="paper-jump-link" href="#dep-key">Key contributions</a>
    </nav>

    <section id="dep-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Cannabis is frequently discussed as a potential mental health aid, but scientific evidence linking cannabis and depression remains inconclusive.</li>
        <li>Twitter contains large volumes of self-reported experiences, yet extracting structured relationships from informal text is technically difficult.</li>
        <li>Standard deep learning models require large annotated datasets, which are costly when domain experts are involved.</li>
        <li>In this study, only <strong>3,000 of 11,000 tweets</strong> were expert-labeled (Cohen's kappa = 0.8), creating a limited supervision setting.</li>
      </ul>
    </section>

    <section id="dep-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>We propose a <strong>knowledge-infused relation extraction model</strong> that combines Drug Abuse Ontology (315 entities, 31 relations), DSM-5 and related clinical lexicons, GPT-3 embeddings, and supervised contrastive learning with triplet loss.</li>
        <li>We extract and classify three relationships between cannabis and depression: <strong>Reason</strong>, <strong>Effect</strong>, and <strong>Addiction</strong>.</li>
        <li>The model reaches an <strong>F1 score of 75.37</strong>, reported as a <strong>+11.28 point</strong> gain over the strongest baseline.</li>
        <li>Ablation results show removing contrastive learning reduces F1 by <strong>6.46</strong> points, and removing knowledge infusion reduces F1 by <strong>9.01</strong> points.</li>
        <li>The learned representation space is then used to label the remaining ~7,000 tweets.</li>
      </ul>

      <figure class="paper-figure">
        <div class="paper-table-wrap" role="region" aria-label="Table I: Performance comparison across baseline models">
          <table class="paper-table">
            <thead>
              <tr>
                <th>Method</th>
                <th>Precision</th>
                <th>Recall</th>
                <th>F1-Score</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>BERT</td>
                <td>64.49</td>
                <td>63.22</td>
                <td>63.85</td>
              </tr>
              <tr>
                <td>BioBERT</td>
                <td>63.97</td>
                <td>62.15</td>
                <td>63.06</td>
              </tr>
              <tr>
                <td>BERT<sub>PE</sub></td>
                <td>60.64</td>
                <td>56.51</td>
                <td>58.50</td>
              </tr>
              <tr>
                <td>BERT<sub>PE+PA</sub></td>
                <td>65.41</td>
                <td>65.25</td>
                <td>64.50</td>
              </tr>
              <tr class="paper-row-highlight">
                <td>Proposed Model</td>
                <td>74.60</td>
                <td>76.17</td>
                <td>75.37</td>
              </tr>
            </tbody>
          </table>
        </div>
        <figcaption>Table I. The proposed model improves F1 to 75.37, exceeding BERT-based baselines by over 11 points.</figcaption>
      </figure>

      <p class="paper-reference">As shown in Table I, the knowledge-infused contrastive approach outperforms all baselines.</p>
    </section>

    <section id="dep-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li><strong>Knowledge-guided phrase extraction:</strong> Map tweet n-grams to cannabis and depression entities using ontology matching (cosine similarity >= 0.75).</li>
        <li><strong>Contextual embeddings:</strong> Use GPT-3 to obtain phrase representations.</li>
        <li><strong>Supervised contrastive learning:</strong> Train anchor-positive-negative triplets to separate relation classes in embedding space.</li>
        <li><strong>Weak supervision extension:</strong> Label the remaining ~7,000 tweets using the learned metric and clustering.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/depression/figure1.png" alt="Knowledge-guided phrase extraction and ontology mapping pipeline for cannabis-depression relation extraction.">
        <figcaption>Figure 1. Knowledge-guided phrase extraction pipeline combining ontology matching and GPT-3 embeddings.</figcaption>
      </figure>

      <p class="paper-reference">The extraction pipeline (Figure 1) shows how ontology-matched phrases are embedded before relation classification.</p>
    </section>

    <section id="dep-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>A knowledge-infused neural model for cannabis-depression relation extraction.</li>
        <li>Integration of GPT-3 embeddings with supervised contrastive learning under limited supervision.</li>
        <li>An absolute <strong>+11.28 F1 improvement</strong> over the strongest BERT-based baseline.</li>
        <li>Release of an annotated dataset covering 3,000 expert-labeled tweets and model-labeled data for the full 11,000 tweet set.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-depression-relations {
      position: relative;
      padding: 0.5rem 0 0.25rem;
      color: var(--global-text-color);
      --paper-ink: var(--global-text-color);
      --paper-ink-soft: var(--global-text-color-light);
      --paper-panel: var(--global-bg-color);
      --paper-border: var(--global-border-color);
      --paper-shadow: 0 14px 30px rgba(0, 0, 0, 0.12);
      --paper-accent: var(--global-link-color);
      --paper-table-even: rgba(0, 0, 0, 0.04);
      --paper-table-border: var(--global-border-color);
    }

    html[data-theme="dark"] .paper-depression-relations {
      --paper-table-even: rgba(255, 255, 255, 0.06);
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.35);
    }

    .paper-depression-relations .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-depression-relations .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.36;
    }

    .paper-depression-relations .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-depression-relations .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.2rem;
    }

    .paper-depression-relations .paper-note {
      margin: 0 0 0.5rem;
      color: var(--paper-ink-soft);
    }

    .paper-depression-relations .paper-jump-links {
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

    .paper-depression-relations .paper-jump-link {
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

    .paper-depression-relations .paper-jump-link:hover,
    .paper-depression-relations .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-depression-relations .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-depression-relations .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-depression-relations .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-depression-relations .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-depression-relations .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-depression-relations .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-depression-relations .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-depression-relations .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-depression-relations .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    html[data-theme="dark"] .paper-depression-relations .paper-figure-architecture img {
      border: 1px solid rgba(255, 255, 255, 0.18);
    }

    .paper-depression-relations .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-depression-relations .paper-table-wrap {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .paper-depression-relations .paper-table {
      width: 100%;
      min-width: 480px;
      border-collapse: collapse;
      font-size: 0.95rem;
    }

    .paper-depression-relations .paper-table th,
    .paper-depression-relations .paper-table td {
      border: 1px solid var(--paper-table-border);
      padding: 0.6rem 0.75rem;
      text-align: left;
    }

    .paper-depression-relations .paper-table thead th {
      background: var(--global-link-color);
      color: var(--global-bg-color);
      font-weight: 700;
      border-bottom: 2px solid var(--paper-table-border);
    }

    .paper-depression-relations .paper-table tbody tr:nth-child(even) {
      background: var(--paper-table-even);
    }

    .paper-depression-relations .paper-row-highlight {
      font-weight: 700;
    }

    .paper-depression-relations .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-depression-relations .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-depression-relations .paper-jump-links {
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

      .paper-depression-relations .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-depression-relations .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-depression-relations .paper-section {
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

      const canvas = document.getElementById("depression-relation-net");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

      let width = 0;
      let height = 0;
      let dpr = 1;
      let palette = null;
      let hubs = null;
      let lanes = [];
      let particles = [];
      let backgroundDots = [];
      let animationId = null;
      let lastFrame = 0;
      let spawnAccumulator = 0;

      const relationDefs = [
        { id: "reason", label: "Reason", offset: -0.19, bend: -0.17 },
        { id: "effect", label: "Effect", offset: 0.0, bend: 0.0 },
        { id: "addiction", label: "Addiction", offset: 0.19, bend: 0.17 }
      ];

      const rand = (min, max) => min + Math.random() * (max - min);
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

      const pointOnQuadratic = (path, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * path.p0.x + 2 * inv * t * path.p1.x + t * t * path.p2.x,
          y: inv * inv * path.p0.y + 2 * inv * t * path.p1.y + t * t * path.p2.y
        };
      };

      const buildPath = (lane) => {
        const yOffset = height * lane.offset;
        const curve = height * lane.bend;
        return {
          p0: { x: hubs.left.x, y: hubs.left.y + yOffset * 0.42 },
          p1: { x: width * 0.5, y: height * 0.5 + curve },
          p2: { x: hubs.right.x, y: hubs.right.y + yOffset * 0.42 }
        };
      };

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bg = parseColor(styles.getPropertyValue("--global-bg-color")) || [242, 242, 242];
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [80, 145, 163];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [52, 56, 63];

        const reason = mixColor(bg, accent, 0.86);
        const effect = mixColor(bg, text, 0.74);
        const addiction = reason.map((channel, index) =>
          Math.round((channel + mixColor(bg, text, 0.58)[index]) * 0.5)
        );

        palette = {
          wash: mixColor(bg, accent, 0.24),
          hub: mixColor(bg, text, 0.66),
          hubInner: mixColor(bg, accent, 0.74),
          dot: mixColor(bg, text, 0.36),
          reason,
          effect,
          addiction,
          label: mixColor(bg, text, 0.78)
        };
      };

      const resetScene = () => {
        hubs = {
          left: { x: width * 0.23, y: height * 0.5 },
          right: { x: width * 0.77, y: height * 0.5 }
        };

        lanes = relationDefs.map((lane) => ({
          ...lane,
          path: buildPath(lane)
        }));

        const dotCount = width < 760 ? 35 : 60;
        backgroundDots = Array.from({ length: dotCount }, () => ({
          x: rand(0, width),
          y: rand(0, height),
          vx: rand(-0.03, 0.03),
          vy: rand(-0.03, 0.03),
          r: rand(0.8, 1.9),
          a: rand(0.06, 0.18)
        }));

        particles = [];
        for (let i = 0; i < 18; i += 1) {
          const lane = lanes[i % lanes.length];
          particles.push({
            laneId: lane.id,
            t: rand(0, 1),
            speed: rand(0.07, 0.15),
            size: rand(1.4, 2.8),
            alpha: rand(0.2, 0.48)
          });
        }
      };

      const relationColor = (laneId) => {
        if (laneId === "reason") {
          return palette.reason;
        }
        if (laneId === "effect") {
          return palette.effect;
        }
        return palette.addiction;
      };

      const spawnParticle = () => {
        const lane = lanes[Math.floor(rand(0, lanes.length))];
        particles.push({
          laneId: lane.id,
          t: 0,
          speed: rand(0.08, 0.16),
          size: rand(1.4, 2.8),
          alpha: rand(0.2, 0.46)
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
        resetScene();
      };

      const drawLane = (lane) => {
        const color = relationColor(lane.id);
        ctx.beginPath();
        ctx.moveTo(lane.path.p0.x, lane.path.p0.y);
        ctx.quadraticCurveTo(lane.path.p1.x, lane.path.p1.y, lane.path.p2.x, lane.path.p2.y);
        ctx.strokeStyle = toRgba(color, 0.4);
        ctx.lineWidth = 2.4;
        ctx.stroke();

        const labelPoint = pointOnQuadratic(lane.path, 0.5);
        ctx.fillStyle = toRgba(color, 0.84);
        ctx.font = "600 12px sans-serif";
        ctx.textAlign = "center";
        ctx.fillText(lane.label, labelPoint.x, labelPoint.y - 10);
      };

      const drawHub = (hub, label) => {
        ctx.beginPath();
        ctx.arc(hub.x, hub.y, 14, 0, Math.PI * 2);
        ctx.fillStyle = toRgba(palette.hub, 0.74);
        ctx.fill();

        ctx.beginPath();
        ctx.arc(hub.x, hub.y, 8, 0, Math.PI * 2);
        ctx.fillStyle = toRgba(palette.hubInner, 0.82);
        ctx.fill();

        ctx.font = "600 13px sans-serif";
        ctx.textAlign = "center";
        ctx.fillStyle = toRgba(palette.label, 0.82);
        ctx.fillText(label, hub.x, hub.y - 20);
      };

      const drawBackground = () => {
        const wash = ctx.createRadialGradient(
          width * 0.5,
          height * 0.5,
          30,
          width * 0.5,
          height * 0.5,
          Math.max(width, height) * 0.7
        );
        wash.addColorStop(0, toRgba(palette.wash, 0.08));
        wash.addColorStop(1, "rgba(0,0,0,0)");
        ctx.fillStyle = wash;
        ctx.fillRect(0, 0, width, height);

        for (const dot of backgroundDots) {
          ctx.beginPath();
          ctx.arc(dot.x, dot.y, dot.r, 0, Math.PI * 2);
          ctx.fillStyle = toRgba(palette.dot, dot.a);
          ctx.fill();
        }
      };

      const findLane = (laneId) => lanes.find((lane) => lane.id === laneId);

      const step = (deltaMs) => {
        const delta = deltaMs / 1000;
        for (const dot of backgroundDots) {
          dot.x += dot.vx * deltaMs;
          dot.y += dot.vy * deltaMs;
          if (dot.x < -5) dot.x = width + 5;
          if (dot.x > width + 5) dot.x = -5;
          if (dot.y < -5) dot.y = height + 5;
          if (dot.y > height + 5) dot.y = -5;
        }

        if (!prefersReducedMotion.matches) {
          spawnAccumulator += deltaMs;
          if (spawnAccumulator > 300) {
            spawnAccumulator = 0;
            spawnParticle();
          }
        }

        for (const packet of particles) {
          packet.t += packet.speed * delta;
        }

        particles = particles.filter((packet) => packet.t <= 1.05);
      };

      const draw = () => {
        ctx.clearRect(0, 0, width, height);
        drawBackground();

        for (const lane of lanes) {
          drawLane(lane);
        }

        drawHub(hubs.left, "Cannabis");
        drawHub(hubs.right, "Depression");

        for (const packet of particles) {
          const lane = findLane(packet.laneId);
          if (!lane) {
            continue;
          }
          const point = pointOnQuadratic(lane.path, clamp(packet.t, 0, 1));
          const color = relationColor(packet.laneId);
          ctx.beginPath();
          ctx.arc(point.x, point.y, packet.size, 0, Math.PI * 2);
          ctx.fillStyle = toRgba(color, packet.alpha);
          ctx.fill();
        }
      };

      const render = (timestamp) => {
        if (!lastFrame) {
          lastFrame = timestamp;
        }
        const deltaMs = Math.min(48, timestamp - lastFrame);
        lastFrame = timestamp;

        step(deltaMs);
        draw();

        if (!prefersReducedMotion.matches) {
          animationId = window.requestAnimationFrame(render);
        } else {
          animationId = null;
        }
      };

      const start = () => {
        window.cancelAnimationFrame(animationId);
        animationId = null;
        lastFrame = 0;
        resize();
        draw();
        if (!prefersReducedMotion.matches) {
          animationId = window.requestAnimationFrame(render);
        }
      };

      const handleMotionChange = () => {
        start();
      };

      window.addEventListener("resize", start, { passive: true });
      if (prefersReducedMotion.addEventListener) {
        prefersReducedMotion.addEventListener("change", handleMotionChange);
      } else if (prefersReducedMotion.addListener) {
        prefersReducedMotion.addListener(handleMotionChange);
      }

      const themeObserver = new MutationObserver((mutations) => {
        for (const mutation of mutations) {
          if (mutation.type === "attributes" && mutation.attributeName === "data-theme") {
            start();
            break;
          }
        }
      });
      themeObserver.observe(root, { attributes: true, attributeFilter: ["data-theme"] });

      window.addEventListener(
        "pagehide",
        () => {
          window.cancelAnimationFrame(animationId);
          themeObserver.disconnect();
        },
        { once: true }
      );

      start();
    })();
  </script>
</div>
