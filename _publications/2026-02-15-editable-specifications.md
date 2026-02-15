---
title: "Toward Neurosymbolic Reinforcement Learning via Editable Specifications"
collection: publications
category: workshops
permalink: /publication/2026-aaai-make-editable-specifications
excerpt: "A neurosymbolic RL framework where editable specifications drive immediate, auditable behavior changes without retraining."
date: 2026-02-15
venue: "AAAI-MAKE 2026 (Under Review)"
paperurl: "https://scholarcommons.sc.edu/cgi/viewcontent.cgi?article=1654&context=aii_fac_pub"
citation: "Vedant Khandelwal, Hong Yung Yip, and Amit Sheth (2026). &quot;Toward Neurosymbolic Reinforcement Learning via Editable Specifications.&quot; <i>Submitted to AAAI-MAKE 2026 (under review)</i>."
header:
  teaser: /images/publications/kgrl/figure1.png
---
<div class="paper-editable-spec">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="constraint-shield-net" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">This paper proposes a practical path for adapting reinforcement learning systems through editable symbolic requirements rather than retraining.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#spec-why">Why</a>
      <a class="paper-jump-link" href="#spec-what">What</a>
      <a class="paper-jump-link" href="#spec-how">How</a>
      <a class="paper-jump-link" href="#spec-key">Key contributions</a>
    </nav>

    <section id="spec-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Reinforcement learning systems are typically adapted through retraining, even when deployment changes are structured requirement updates like revised safety rules or updated operational constraints.</li>
        <li>This adaptation primitive is expensive, hard to audit, and can entangle unintended behavioral shifts with intended changes.</li>
        <li>In real deployments, many updates are local and human-legible edits, such as forbidding an action under a mode switch or changing energy-speed tradeoffs.</li>
        <li>Those edits should produce immediate and inspectable behavioral effects without requiring gradient updates.</li>
      </ul>
    </section>

    <section id="spec-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <p>We treat an <strong>editable specification</strong> as a first-class interface for adaptation. The specification is represented as:</p>

      <div class="paper-equation"><code>G = (R, C, P)</code></div>

      <ul class="paper-list">
        <li><code>R</code> defines action applicability rules.</li>
        <li><code>C</code> defines hard constraints (forbidden behavior).</li>
        <li><code>P</code> defines soft preferences (tradeoffs).</li>
      </ul>

      <p>The policy is conditioned on <code>G</code> at execution time, while enforcement and preference shaping are applied directly in the decision loop.</p>

      <div class="paper-equation"><code>A_G(s) = {a in A | C(s, a, G) = 0}</code></div>
      <div class="paper-equation"><code>r_G(s, a) = r(s, a) - lambda * c_P(s, a, G)</code></div>

      <p>Requirement updates are modeled as edits <code>G' = Delta(G)</code>, enabling immediate behavioral changes for in-schema edits with zero gradient updates.</p>
    </section>

    <section id="spec-how" class="paper-section paper-anchor">
      <h2>How it works (high level)</h2>
      <ul class="paper-list">
        <li>Maintain a persistent knowledge graph <code>G = (R, C, P)</code> with local edit operations and provenance tracking.</li>
        <li>Condition the policy <code>pi_theta(a | s, G)</code> on the specification (optionally via graph embedding).</li>
        <li>Enforce hard constraints via runtime shielding (action masking or safe-set projection).</li>
        <li>Apply soft preferences through reward shaping or action reweighting.</li>
        <li>When requirements change, apply an edit <code>Delta</code> to produce <code>G'</code>; the next decision step recomputes feasibility and preferences without modifying policy parameters.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/kgrl/figure1.png" alt="Reference architecture for editable specifications in reinforcement learning.">
        <figcaption>Figure 1. Editable specifications update behavior at runtime via shielding and shaping without modifying policy parameters.</figcaption>
      </figure>

      <p class="paper-reference">Figure 1 illustrates how specification edits flow directly into constraint enforcement and preference shaping in the execution loop.</p>
    </section>

    <section id="spec-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduces <strong>editable knowledge-graph specifications</strong> as an operational interface for RL adaptation.</li>
        <li>Formalizes execution-time semantics where constraint edits deterministically change the feasible action set.</li>
        <li>Separates competence (learned policy) from compliance (runtime shielding and preference shaping).</li>
        <li>Defines an <strong>edit-based generalization objective</strong>, evaluating post-edit success without retraining.</li>
        <li>Positions auditability and requirement traceability as core properties of neurosymbolic RL systems.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-editable-spec {
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

    html[data-theme="dark"] .paper-editable-spec {
      --paper-shadow: 0 16px 34px rgba(0, 0, 0, 0.33);
    }

    .paper-editable-spec .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-editable-spec .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.36;
    }

    .paper-editable-spec .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-editable-spec .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.3rem;
    }

    .paper-editable-spec .paper-note {
      margin: 0 0 0.4rem;
      color: var(--paper-ink-soft);
    }

    .paper-editable-spec .paper-jump-links {
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

    .paper-editable-spec .paper-jump-link {
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

    .paper-editable-spec .paper-jump-link:hover,
    .paper-editable-spec .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-editable-spec .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-editable-spec .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-editable-spec .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-editable-spec .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-editable-spec .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), transparent);
    }

    .paper-editable-spec .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-editable-spec .paper-equation {
      margin: 0.9rem 0;
      padding: 0.55rem 0.7rem;
      border: 1px solid var(--paper-border);
      border-radius: 10px;
      background: color-mix(in srgb, var(--paper-panel) 92%, transparent);
      font-size: 0.98rem;
      overflow-x: auto;
    }

    .paper-editable-spec .paper-equation code {
      background: transparent;
      padding: 0;
      color: var(--paper-ink);
      white-space: nowrap;
    }

    .paper-editable-spec .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-editable-spec .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-editable-spec .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    html[data-theme="dark"] .paper-editable-spec .paper-figure-architecture img {
      border: 1px solid rgba(255, 255, 255, 0.18);
    }

    .paper-editable-spec .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-editable-spec .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-editable-spec .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-editable-spec .paper-jump-links {
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

      .paper-editable-spec .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-editable-spec .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-editable-spec .paper-section {
        padding: 1.2rem 1.1rem;
      }

      .paper-editable-spec .paper-equation {
        font-size: 0.92rem;
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

      const canvas = document.getElementById("constraint-shield-net");
      if (!canvas) {
        return;
      }

      const ctx = canvas.getContext("2d", { alpha: true });
      if (!ctx) {
        return;
      }

      const root = document.documentElement;
      const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

      const rowRatios = [0.22, 0.5, 0.78];
      const colRatios = [0.12, 0.37, 0.62, 0.87];
      const actions = [
        { id: "fast", label: "Fast", delta: -1, curve: -0.58 },
        { id: "balance", label: "Balance", delta: 0, curve: 0 },
        { id: "safe", label: "Safe", delta: 1, curve: 0.58 }
      ];

      const PLAN_MS = 1250;
      const MOVE_MS = 1300;
      const BLOCK_T = 0.24;

      let width = 0;
      let height = 0;
      let dpr = 1;
      let palette = null;

      let nodes = [];
      let nodeGrid = [];
      let edges = [];
      let outgoingByNode = new Map();

      let currentNode = null;
      let decision = null;
      let phase = "plan";
      let phaseTime = 0;
      let stepCounter = 0;
      let stepsUntilEdit = 2;
      let animationId = null;
      let lastFrame = 0;
      let nowTime = 0;

      const spec = {
        hardMasks: [],
        softWeights: { fast: 1.12, balance: 1.0, safe: 1.08 },
        message: "Baseline specification",
        messageUntil: 0,
        editedNodeId: null,
        editedUntil: 0
      };

      const rand = (min, max) => min + Math.random() * (max - min);
      const randInt = (min, max) => Math.floor(rand(min, max + 1));
      const clamp = (value, min, max) => Math.max(min, Math.min(max, value));
      const easeInOut = (t) => t * t * (3 - 2 * t);

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
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [80, 145, 163];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [52, 56, 63];

        palette = {
          wash: mixColor(bg, accent, 0.27),
          node: mixColor(bg, text, 0.53),
          nodeSoft: mixColor(bg, text, 0.34),
          nodeActive: mixColor(bg, accent, 0.72),
          nodeEdited: mixColor(bg, accent, 0.86),
          edgeCandidate: mixColor(bg, text, 0.36),
          edgeFeasible: mixColor(bg, accent, 0.66),
          edgeMasked: mixColor(bg, text, 0.56),
          proposed: mixColor(bg, text, 0.72),
          chosen: mixColor(bg, accent, 0.88),
          shield: mixColor(bg, accent, 0.95),
          panel: mixColor(bg, text, 0.16),
          panelBorder: mixColor(bg, text, 0.24),
          panelText: mixColor(bg, text, 0.7)
        };
      };

      const getNodePosition = (node) => ({
        x: node.xRatio * width,
        y: node.yRatio * height
      });

      const getEdgeGeometry = (edge) => {
        const start = getNodePosition(edge.from);
        const end = getNodePosition(edge.to);
        const dx = end.x - start.x;
        const dy = end.y - start.y;
        const len = Math.max(1, Math.hypot(dx, dy));
        const nx = -dy / len;
        const ny = dx / len;
        const bend = edge.curve * len * 0.16;
        return {
          start,
          end,
          control: {
            x: (start.x + end.x) * 0.5 + nx * bend,
            y: (start.y + end.y) * 0.5 + ny * bend
          }
        };
      };

      const pointOnQuadratic = (p0, p1, p2, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * p0.x + 2 * inv * t * p1.x + t * t * p2.x,
          y: inv * inv * p0.y + 2 * inv * t * p1.y + t * t * p2.y
        };
      };

      const drawCurve = (geometry) => {
        ctx.moveTo(geometry.start.x, geometry.start.y);
        ctx.quadraticCurveTo(
          geometry.control.x,
          geometry.control.y,
          geometry.end.x,
          geometry.end.y
        );
      };

      const drawPartialCurve = (geometry, tEnd) => {
        const steps = 18;
        const limit = clamp(tEnd, 0, 1);
        ctx.moveTo(geometry.start.x, geometry.start.y);
        for (let i = 1; i <= steps; i += 1) {
          const t = limit * (i / steps);
          const point = pointOnQuadratic(geometry.start, geometry.control, geometry.end, t);
          ctx.lineTo(point.x, point.y);
        }
      };

      const drawArrowHead = (geometry, color, alpha, size = 5) => {
        const tip = pointOnQuadratic(geometry.start, geometry.control, geometry.end, 0.985);
        const prev = pointOnQuadratic(geometry.start, geometry.control, geometry.end, 0.94);
        const angle = Math.atan2(tip.y - prev.y, tip.x - prev.x);
        ctx.fillStyle = toRgba(color, alpha);
        ctx.beginPath();
        ctx.moveTo(tip.x, tip.y);
        ctx.lineTo(
          tip.x - Math.cos(angle - Math.PI / 8) * size,
          tip.y - Math.sin(angle - Math.PI / 8) * size
        );
        ctx.lineTo(
          tip.x - Math.cos(angle + Math.PI / 8) * size,
          tip.y - Math.sin(angle + Math.PI / 8) * size
        );
        ctx.closePath();
        ctx.fill();
      };

      const buildGraph = () => {
        nodeGrid = colRatios.map((xRatio, col) =>
          rowRatios.map((yRatio, row) => ({
            id: `s-${col}-${row}`,
            col,
            row,
            xRatio,
            yRatio,
            radius: rand(3.7, 4.6)
          }))
        );
        nodes = nodeGrid.flat();

        edges = [];
        outgoingByNode = new Map();
        for (let col = 0; col < colRatios.length - 1; col += 1) {
          for (let row = 0; row < rowRatios.length; row += 1) {
            const from = nodeGrid[col][row];
            const outgoing = [];
            actions.forEach((action) => {
              const nextRow = clamp(row + action.delta, 0, rowRatios.length - 1);
              const to = nodeGrid[col + 1][nextRow];
              const edge = {
                id: `${from.id}-${action.id}`,
                from,
                to,
                actionId: action.id,
                actionLabel: action.label,
                curve: action.curve,
                bias: rand(0.86, 1.2),
                phase: rand(0, Math.PI * 2)
              };
              edges.push(edge);
              outgoing.push(edge);
            });
            outgoingByNode.set(from.id, outgoing);
          }
        }
      };

      const initializeSpec = () => {
        spec.hardMasks = rowRatios.map(() => new Set());
        spec.softWeights = { fast: 1.12, balance: 1.0, safe: 1.08 };
        spec.message = "Baseline specification";
        spec.messageUntil = nowTime + 2000;
        spec.editedNodeId = null;
        spec.editedUntil = 0;
      };

      const ensureFeasibleMask = (row) => {
        const set = spec.hardMasks[row];
        if (set.size >= actions.length) {
          const remove = actions[Math.floor(Math.random() * actions.length)].id;
          set.delete(remove);
        }
      };

      const applySpecEdit = () => {
        const row = randInt(0, rowRatios.length - 1);
        const action = actions[randInt(0, actions.length - 1)];
        const editType = randInt(0, 2);
        const modeName = `mode ${row + 1}`;

        if (editType === 0) {
          const set = spec.hardMasks[row];
          if (set.has(action.id)) {
            set.delete(action.id);
            spec.message = `Delta: allow ${action.label} in ${modeName}`;
          } else {
            if (set.size >= actions.length - 1) {
              const removable = Array.from(set).filter((id) => id !== action.id);
              if (removable.length) {
                set.delete(removable[randInt(0, removable.length - 1)]);
              }
            }
            set.add(action.id);
            ensureFeasibleMask(row);
            spec.message = `Delta: forbid ${action.label} in ${modeName}`;
          }
          spec.editedNodeId = `s-${Math.min(currentNode.col + 1, colRatios.length - 1)}-${row}`;
        } else if (editType === 1) {
          spec.softWeights = { fast: 1.36, balance: 1.0, safe: 0.82 };
          spec.message = "Delta: preference shift toward speed";
          spec.editedNodeId = currentNode.id;
        } else {
          spec.softWeights = { fast: 0.8, balance: 1.05, safe: 1.34 };
          spec.message = "Delta: preference shift toward safety";
          spec.editedNodeId = currentNode.id;
        }

        spec.messageUntil = nowTime + 2600;
        spec.editedUntil = nowTime + 1500;
      };

      const evaluateCurrentStep = () => {
        const activeEdges = outgoingByNode.get(currentNode.id) || [];
        const rowMask = spec.hardMasks[currentNode.row];

        const evaluations = activeEdges.map((edge) => {
          const policyScore = edge.bias + Math.sin(nowTime * 0.001 + edge.phase) * 0.16 + rand(-0.05, 0.05);
          const feasible = !rowMask.has(edge.actionId);
          const utility = policyScore * (spec.softWeights[edge.actionId] || 1);
          return { edge, policyScore, utility, feasible };
        });

        const proposed = evaluations.reduce(
          (best, item) => (item.policyScore > best.policyScore ? item : best),
          evaluations[0]
        );
        const feasibleEvaluations = evaluations.filter((item) => item.feasible);
        const chosen = feasibleEvaluations.length
          ? feasibleEvaluations.reduce(
              (best, item) => (item.utility > best.utility ? item : best),
              feasibleEvaluations[0]
            )
          : proposed;

        decision = {
          evaluations,
          proposed,
          chosen,
          blocked: !proposed.feasible,
          feasibleCount: feasibleEvaluations.length
        };
      };

      const drawBackdrop = () => {
        const radial = ctx.createRadialGradient(
          width * 0.52,
          height * 0.5,
          40,
          width * 0.52,
          height * 0.5,
          Math.max(width, height) * 0.72
        );
        radial.addColorStop(0, toRgba(palette.wash, 0.08));
        radial.addColorStop(1, "rgba(0, 0, 0, 0)");
        ctx.fillStyle = radial;
        ctx.fillRect(0, 0, width, height);
      };

      const drawBaseGraph = () => {
        ctx.lineCap = "round";
        ctx.setLineDash([4, 9]);
        ctx.strokeStyle = toRgba(palette.edgeCandidate, 0.14);
        ctx.lineWidth = 0.9;
        edges.forEach((edge) => {
          const geometry = getEdgeGeometry(edge);
          ctx.beginPath();
          drawCurve(geometry);
          ctx.stroke();
        });
        ctx.setLineDash([]);
      };

      const drawDecisionEdges = () => {
        if (!decision) {
          return;
        }

        decision.evaluations.forEach((item) => {
          const geometry = getEdgeGeometry(item.edge);
          const weight = spec.softWeights[item.edge.actionId] || 1;
          if (item.feasible) {
            ctx.strokeStyle = toRgba(palette.edgeFeasible, 0.34 + 0.08 * weight);
            ctx.lineWidth = 1.2 + 0.75 * weight;
            ctx.beginPath();
            drawCurve(geometry);
            ctx.stroke();
            drawArrowHead(geometry, palette.edgeFeasible, 0.4, 5.3);
          } else {
            ctx.setLineDash([6, 5]);
            ctx.strokeStyle = toRgba(palette.edgeMasked, 0.32);
            ctx.lineWidth = 1.2;
            ctx.beginPath();
            drawCurve(geometry);
            ctx.stroke();
            ctx.setLineDash([]);
            drawArrowHead(geometry, palette.edgeMasked, 0.2, 4.8);
          }

          if (item.edge.id === decision.proposed.edge.id) {
            ctx.strokeStyle = toRgba(palette.proposed, 0.36);
            ctx.lineWidth = 1;
            ctx.beginPath();
            drawCurve(geometry);
            ctx.stroke();
          }
        });
      };

      const drawNodes = () => {
        nodes.forEach((node) => {
          const position = getNodePosition(node);
          const isCurrent = currentNode && node.id === currentNode.id;
          const isEdited = spec.editedNodeId === node.id && spec.editedUntil > nowTime;
          const editPulse = isEdited ? 1 - (spec.editedUntil - nowTime) / 1500 : 0;

          ctx.fillStyle = toRgba(
            isEdited ? palette.nodeEdited : isCurrent ? palette.nodeActive : palette.node,
            isCurrent || isEdited ? 0.44 : 0.26
          );
          ctx.beginPath();
          ctx.arc(position.x, position.y, node.radius + (isCurrent ? 1.1 : 0), 0, Math.PI * 2);
          ctx.fill();

          ctx.strokeStyle = toRgba(palette.nodeSoft, 0.38);
          ctx.lineWidth = 1;
          ctx.beginPath();
          ctx.arc(position.x, position.y, node.radius + 1.7, 0, Math.PI * 2);
          ctx.stroke();

          if (isEdited) {
            ctx.strokeStyle = toRgba(palette.nodeEdited, 0.2 + (1 - editPulse) * 0.25);
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.arc(position.x, position.y, node.radius + 4 + editPulse * 10, 0, Math.PI * 2);
            ctx.stroke();
          }
        });
      };

      const drawMotion = () => {
        if (!decision) {
          return;
        }

        const chosenGeometry = getEdgeGeometry(decision.chosen.edge);
        const moveProgress = phase === "move" ? easeInOut(clamp(phaseTime / MOVE_MS, 0, 1)) : 0;
        const chosenPoint = pointOnQuadratic(
          chosenGeometry.start,
          chosenGeometry.control,
          chosenGeometry.end,
          phase === "move" ? moveProgress : 0
        );

        if (phase === "plan") {
          const pulse = 0.16 + 0.1 * Math.sin(nowTime * 0.008);
          decision.evaluations.forEach((item, index) => {
            const geometry = getEdgeGeometry(item.edge);
            const t = 0.1 + ((nowTime * 0.00025 + index * 0.22) % 0.18);
            const point = pointOnQuadratic(geometry.start, geometry.control, geometry.end, t);
            ctx.fillStyle = toRgba(item.feasible ? palette.chosen : palette.proposed, pulse);
            ctx.beginPath();
            ctx.arc(point.x, point.y, 1.6, 0, Math.PI * 2);
            ctx.fill();
          });
        }

        if (phase === "move" && decision.blocked) {
          const proposedGeometry = getEdgeGeometry(decision.proposed.edge);
          const blockedTravel = Math.min(BLOCK_T, moveProgress * 1.45);
          ctx.strokeStyle = toRgba(palette.proposed, 0.45);
          ctx.lineWidth = 1.2;
          ctx.beginPath();
          drawPartialCurve(proposedGeometry, blockedTravel);
          ctx.stroke();

          const shieldPoint = pointOnQuadratic(
            proposedGeometry.start,
            proposedGeometry.control,
            proposedGeometry.end,
            BLOCK_T
          );
          if (moveProgress > 0.15) {
            const pulse = (moveProgress - 0.15) / 0.85;
            ctx.strokeStyle = toRgba(palette.shield, 0.2 + (1 - pulse) * 0.24);
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.arc(shieldPoint.x, shieldPoint.y, 5 + pulse * 9, 0, Math.PI * 2);
            ctx.stroke();
          }
        }

        ctx.fillStyle = toRgba(palette.chosen, 0.8);
        ctx.beginPath();
        ctx.arc(chosenPoint.x, chosenPoint.y, 2.5, 0, Math.PI * 2);
        ctx.fill();
      };

      const drawRoundedRectPath = (x, y, w, h, r) => {
        const radius = Math.min(r, w * 0.5, h * 0.5);
        if (typeof ctx.roundRect === "function") {
          ctx.beginPath();
          ctx.roundRect(x, y, w, h, radius);
          return;
        }
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

      const drawHud = () => {
        if (!decision) {
          return;
        }

        const panelWidth = Math.min(width * 0.48, 460);
        const panelHeight = 84;
        const x = 20;
        const y = 18;

        ctx.fillStyle = toRgba(palette.panel, 0.13);
        ctx.strokeStyle = toRgba(palette.panelBorder, 0.28);
        ctx.lineWidth = 1;
        drawRoundedRectPath(x, y, panelWidth, panelHeight, 10);
        ctx.fill();
        ctx.stroke();

        ctx.fillStyle = toRgba(palette.panelText, 0.65);
        ctx.font = "600 12px system-ui, -apple-system, Segoe UI, sans-serif";
        ctx.fillText("Constraint Shield in Motion", x + 12, y + 22);

        const line2 = `A_G(s): ${decision.feasibleCount}/${decision.evaluations.length} feasible  |  Proposal: ${decision.proposed.edge.actionLabel}`;
        const line3 = decision.blocked
          ? `Shield: blocked ${decision.proposed.edge.actionLabel}, executed ${decision.chosen.edge.actionLabel}`
          : `Shield: proposal already feasible`;
        const editLabel = spec.messageUntil > nowTime ? `Edit: ${spec.message}` : "Edit: waiting for next Delta";

        ctx.font = "11px system-ui, -apple-system, Segoe UI, sans-serif";
        ctx.fillText(line2, x + 12, y + 42);
        ctx.fillText(line3, x + 12, y + 60);
        ctx.fillStyle = toRgba(
          spec.messageUntil > nowTime ? palette.nodeEdited : palette.panelText,
          spec.messageUntil > nowTime ? 0.62 : 0.52
        );
        ctx.fillText(editLabel, x + 12, y + 76);
      };

      const drawFrame = () => {
        ctx.clearRect(0, 0, width, height);
        drawBackdrop();
        drawBaseGraph();
        drawDecisionEdges();
        drawMotion();
        drawNodes();
        drawHud();
      };

      const advanceSimulation = (dt) => {
        nowTime += dt;
        phaseTime += dt;

        if (phase === "plan" && phaseTime >= PLAN_MS) {
          phase = "move";
          phaseTime = 0;
          return;
        }

        if (phase === "move" && phaseTime >= MOVE_MS) {
          currentNode = decision.chosen.edge.to;
          if (currentNode.col === colRatios.length - 1) {
            currentNode = nodeGrid[0][currentNode.row];
          }

          stepCounter += 1;
          stepsUntilEdit -= 1;
          if (stepsUntilEdit <= 0) {
            applySpecEdit();
            stepsUntilEdit = randInt(2, 4);
          }

          evaluateCurrentStep();
          phase = "plan";
          phaseTime = 0;
        }
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

      const start = () => {
        if (animationId) {
          window.cancelAnimationFrame(animationId);
          animationId = null;
        }

        updatePalette();
        resize();
        buildGraph();
        initializeSpec();

        currentNode = nodeGrid[0][1];
        phase = "plan";
        phaseTime = 0;
        stepCounter = 0;
        stepsUntilEdit = randInt(2, 4);
        nowTime = 0;
        lastFrame = 0;
        evaluateCurrentStep();
        drawFrame();

        if (!prefersReducedMotion.matches) {
          const loop = (timestamp) => {
            const dt = lastFrame ? Math.min(34, timestamp - lastFrame) : 16;
            lastFrame = timestamp;
            advanceSimulation(dt);
            drawFrame();
            animationId = window.requestAnimationFrame(loop);
          };
          animationId = window.requestAnimationFrame(loop);
        }
      };

      window.addEventListener(
        "resize",
        () => {
          resize();
          drawFrame();
        },
        { passive: true }
      );

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

      start();
    })();
  </script>
</div>
