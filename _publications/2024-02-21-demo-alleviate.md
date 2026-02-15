---
title: "Demo Alleviate: Demonstrating Artificial Intelligence Enabled Virtual Assistance for Telehealth: The Mental Health Case"
collection: publications
category: conferences
permalink: /publication/2024-aaai-demo-alleviate
excerpt: "Alleviate is a safety-constrained telehealth mental-health assistant that combines personalized patient knowledge graphs with explainable feedback loops."
date: 2023-06-26
venue: "Proceedings of the AAAI Conference on Artificial Intelligence (AAAI-23 Demo Track)"
paperurl: "https://ojs.aaai.org/index.php/AAAI/article/view/27085"
citation: "Kaushik Roy, Vedant Khandelwal, Raxit Goswami, Nathan Dolbir, Jinendra Malekar, and Amit Sheth. (2023). &quot;Demo Alleviate: Demonstrating Artificial Intelligence Enabled Virtual Assistance for Telehealth: The Mental Health Case.&quot; <i>Proceedings of the AAAI Conference on Artificial Intelligence</i> 37(13): 16289-16290."
header:
  teaser: /images/publications/mhchat/figure1.png
---

<div class="paper-demo-alleviate">
  <div class="paper-bg" aria-hidden="true">
    <canvas id="mh-alleviate-bg" role="presentation"></canvas>
  </div>

  <div class="paper-content">
    <p class="paper-lede">Alleviate is an AI-enabled telehealth assistant for mental healthcare that couples personalized knowledge representation with medically grounded safety constraints and explainable refinement.</p>

    <nav class="paper-jump-links" aria-label="Publication section navigation">
      <a class="paper-jump-link" href="#mh-why">Why</a>
      <a class="paper-jump-link" href="#mh-what">What</a>
      <a class="paper-jump-link" href="#mh-how">How</a>
      <a class="paper-jump-link" href="#mh-key">Key contributions</a>
    </nav>

    <section id="mh-why" class="paper-section paper-anchor">
      <h2>Why it matters</h2>
      <ul class="paper-list">
        <li>Mental healthcare demand increased significantly following the pandemic, while clinician availability decreased.</li>
        <li>Existing chatbots primarily rely on scripted tasks (for example, reminders and scheduling) and lack deep personalization.</li>
        <li>Safe mental-health assistance requires strict adherence to medically established guidelines.</li>
        <li>Clinicians need AI systems that provide explainable reasoning and integrate structured medical knowledge with patient-specific data.</li>
        <li>Emergency-risk detection (for example, suicidal ideation) requires structured and reliable monitoring mechanisms.</li>
      </ul>
    </section>

    <section id="mh-what" class="paper-section paper-anchor">
      <h2>What we did</h2>
      <ul class="paper-list">
        <li>Proposed <strong>Alleviate</strong>, a mental-health chatbot designed to assist patients and clinicians.</li>
        <li>Represented patient information as a <strong>personalized knowledge graph</strong> integrating provider notes, chatbot interactions, and clinically validated knowledge bases.</li>
        <li>Enforced safety using <strong>graph and tree path constraints</strong> aligned with medical guidelines.</li>
        <li>Used <strong>dense representation similarity</strong> to align patient entities with external medical knowledge (for example, medication interactions).</li>
        <li>Incorporated <strong>explainable reinforcement learning</strong> to support feedback-based refinement.</li>
        <li>Included modules for safe and explainable medication reminders, appraisal of adherence to recommendations, and detection of behaviors requiring emergency human intervention.</li>
      </ul>

      <figure class="paper-figure paper-figure-architecture">
        <img src="/images/publications/mhchat/figure1.png" alt="Alleviate system architecture integrating patient data, domain-specific medical knowledge, and safety-constrained reasoning loops.">
        <figcaption>Figure 1. Alleviate integrates patient data with domain-specific medical knowledge and enforces safety through graph-based constraints and feedback loops.</figcaption>
      </figure>

      <p class="paper-reference">The overall architecture is illustrated in Figure 1, showing how patient data, medical knowledge, and safety constraints are integrated.</p>
    </section>

    <section id="mh-how" class="paper-section paper-anchor">
      <h2>How it works</h2>
      <ul class="paper-list">
        <li><strong>Personalized Knowledge Graph Construction:</strong> extracts &lang;subject, predicate, object&rang; triples from provider notes and conversations to build a patient-specific graph.</li>
        <li><strong>Knowledge Integration:</strong> aligns patient entities with external medical knowledge bases using dense representation similarity.</li>
        <li><strong>Safety-Constrained Reasoning:</strong> enforces clinical guidelines via graph and tree path constraints.</li>
        <li><strong>Explainable RL Refinement:</strong> uses reinforcement learning with clinician feedback for iterative improvement.</li>
        <li><strong>Emergency Detection:</strong> matches conversation patterns against clinically established alarming-behavior questionnaires to trigger human intervention when necessary.</li>
      </ul>

      <figure class="paper-figure">
        <img src="/images/publications/mhchat/figure2.png" alt="Emergency intervention flow where alarming behavioral patterns trigger escalation to human clinicians.">
        <figcaption>Figure 2. Alleviate monitors conversation patterns and triggers emergency intervention when suicidal ideation patterns are detected.</figcaption>
      </figure>

      <p class="paper-reference">Figure 2 demonstrates how the system identifies alarming behavioral patterns and escalates appropriately.</p>
    </section>

    <section id="mh-key" class="paper-section paper-anchor">
      <h2>Key contributions</h2>
      <ul class="paper-list">
        <li>Introduces a graph-based framework integrating patient-specific data with clinically validated mental-health knowledge sources.</li>
        <li>Formalizes safety enforcement using graph and tree path constraints aligned with medical guidelines.</li>
        <li>Implements explainable reinforcement learning for feedback-based refinement.</li>
        <li>Demonstrates integrated modules for medication support, adherence appraisal, and emergency behavior detection.</li>
      </ul>
    </section>
  </div>

  <style>
    .paper-demo-alleviate {
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
    }

    html[data-theme="dark"] .paper-demo-alleviate {
      --paper-shadow: 0 18px 38px rgba(0, 0, 0, 0.35);
    }

    .paper-demo-alleviate .paper-bg {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background: transparent;
    }

    .paper-demo-alleviate .paper-bg canvas {
      display: block;
      width: 100%;
      height: 100%;
      opacity: 0.36;
    }

    .paper-demo-alleviate .paper-content {
      position: relative;
      z-index: 1;
      padding-bottom: 5.8rem;
    }

    .paper-demo-alleviate .paper-lede {
      font-size: 1.05rem;
      font-weight: 600;
      color: var(--paper-ink);
      margin-bottom: 0.35rem;
    }

    .paper-demo-alleviate .paper-jump-links {
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

    .paper-demo-alleviate .paper-jump-link {
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

    .paper-demo-alleviate .paper-jump-link:hover,
    .paper-demo-alleviate .paper-jump-link:focus-visible {
      border-color: var(--paper-accent);
      color: var(--paper-accent);
      outline: none;
    }

    .paper-demo-alleviate .paper-anchor,
    .page__content #paper-citation {
      scroll-margin-top: 95px;
    }

    .paper-demo-alleviate .paper-section {
      margin: 1.75rem 0;
      padding: 1.4rem 1.5rem;
      border-radius: 16px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 86%, transparent);
      box-shadow: var(--paper-shadow);
      backdrop-filter: blur(6px);
    }

    html[data-theme="dark"] .paper-demo-alleviate .paper-section {
      background: color-mix(in srgb, var(--paper-panel) 82%, transparent);
    }

    .paper-demo-alleviate .paper-section h2 {
      position: relative;
      margin-top: 0;
      padding-bottom: 0.6rem;
      color: var(--paper-ink);
    }

    .paper-demo-alleviate .paper-section h2::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0.1rem;
      width: 100%;
      height: 2px;
      background: linear-gradient(90deg, var(--paper-accent), var(--paper-accent-soft));
    }

    .paper-demo-alleviate .paper-list {
      margin: 0.75rem 0 0;
      padding-left: 1.2rem;
    }

    .paper-demo-alleviate .paper-figure {
      margin: 1.5rem 0;
      padding: 1rem;
      border-radius: 12px;
      border: 1px solid var(--paper-border);
      background: color-mix(in srgb, var(--paper-panel) 90%, transparent);
    }

    .paper-demo-alleviate .paper-figure img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .paper-demo-alleviate .paper-figure-architecture img {
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      box-sizing: border-box;
      padding: 0.75rem;
    }

    html[data-theme="dark"] .paper-demo-alleviate .paper-figure-architecture img {
      border: 1px solid rgba(255, 255, 255, 0.18);
    }

    .paper-demo-alleviate .paper-figure figcaption {
      margin-top: 0.75rem;
      font-size: 0.95rem;
      color: var(--paper-ink);
    }

    .paper-demo-alleviate .paper-reference {
      margin-top: 0;
      color: var(--paper-ink);
      font-weight: 600;
    }

    @media (max-width: 720px) {
      .paper-demo-alleviate .paper-content {
        padding-bottom: 6.3rem;
      }

      .paper-demo-alleviate .paper-jump-links {
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

      .paper-demo-alleviate .paper-jump-links::-webkit-scrollbar {
        display: none;
      }

      .paper-demo-alleviate .paper-jump-link {
        display: inline-block;
        font-size: 0.82rem;
        padding: 0.32rem 0.62rem;
      }

      .paper-demo-alleviate .paper-section {
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

      const canvas = document.getElementById("mh-alleviate-bg");
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
      let geometry = null;
      let animationId = null;
      let lastFrame = 0;
      let timeline = 0;

      let intakePackets = [];
      let supportPackets = [];
      let carePackets = [];
      let alertSignals = [];

      const timers = {
        intake: 0,
        support: 0,
        care: 0,
        alert: 0
      };

      const rand = (min, max) => min + Math.random() * (max - min);

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

      const quadraticPoint = (path, t) => {
        const inv = 1 - t;
        return {
          x: inv * inv * path.p0.x + 2 * inv * t * path.p1.x + t * t * path.p2.x,
          y: inv * inv * path.p0.y + 2 * inv * t * path.p1.y + t * t * path.p2.y
        };
      };

      const drawPath = (path) => {
        ctx.moveTo(path.p0.x, path.p0.y);
        ctx.quadraticCurveTo(path.p1.x, path.p1.y, path.p2.x, path.p2.y);
      };

      const drawArrowHead = (path, color, alpha) => {
        const tip = quadraticPoint(path, 1);
        const prev = quadraticPoint(path, 0.96);
        const angle = Math.atan2(tip.y - prev.y, tip.x - prev.x);
        const size = 6;
        ctx.fillStyle = toRgba(color, alpha);
        ctx.beginPath();
        ctx.moveTo(tip.x, tip.y);
        ctx.lineTo(tip.x - Math.cos(angle - Math.PI / 7) * size, tip.y - Math.sin(angle - Math.PI / 7) * size);
        ctx.lineTo(tip.x - Math.cos(angle + Math.PI / 7) * size, tip.y - Math.sin(angle + Math.PI / 7) * size);
        ctx.closePath();
        ctx.fill();
      };

      const updatePalette = () => {
        const styles = getComputedStyle(root);
        const bg = parseColor(styles.getPropertyValue("--global-bg-color")) || [242, 242, 242];
        const accent = parseColor(styles.getPropertyValue("--global-link-color")) || [87, 151, 176];
        const text = parseColor(styles.getPropertyValue("--global-text-color")) || [54, 59, 66];

        palette = {
          wash: mixColor(bg, accent, 0.24),
          laneSoft: mixColor(bg, accent, 0.18),
          lane: mixColor(bg, accent, 0.4),
          monitor: mixColor(bg, accent, 0.7),
          monitorSoft: mixColor(bg, accent, 0.36),
          node: mixColor(bg, text, 0.52),
          nodeSoft: mixColor(bg, accent, 0.5),
          intake: mixColor(bg, accent, 0.76),
          support: mixColor(bg, text, 0.68),
          care: mixColor(bg, accent, 0.62),
          alert: [223, 96, 78]
        };
      };

      const buildGeometry = () => {
        const xPatient = width * 0.2;
        const xBot = width * 0.5;
        const xClinician = width * 0.8;
        const yMid = height * 0.52;

        geometry = {
          xPatient,
          xBot,
          xClinician,
          yMid,
          monitorY: height * 0.86,
          patientToBot: {
            p0: { x: xPatient, y: yMid + 10 },
            p1: { x: width * 0.34, y: yMid - 92 },
            p2: { x: xBot, y: yMid + 4 }
          },
          botToSupport: {
            p0: { x: xBot, y: yMid + 2 },
            p1: { x: width * 0.36, y: yMid + 118 },
            p2: { x: xPatient, y: yMid + 40 }
          },
          botToClinician: {
            p0: { x: xBot, y: yMid - 2 },
            p1: { x: width * 0.66, y: yMid - 106 },
            p2: { x: xClinician, y: yMid + 8 }
          },
          alertPath: {
            p0: { x: xBot, y: yMid - 2 },
            p1: { x: xBot + 10, y: height * 0.26 },
            p2: { x: xClinician - 16, y: height * 0.18 }
          }
        };
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
        buildGeometry();
      };

      const spawnPacket = (collection, durationMin, durationMax, radiusMin, radiusMax) => {
        collection.push({
          t: 0,
          duration: rand(durationMin, durationMax),
          radius: rand(radiusMin, radiusMax),
          alpha: rand(0.24, 0.42)
        });
      };

      const seedScene = () => {
        intakePackets = [];
        supportPackets = [];
        carePackets = [];
        alertSignals = [];

        for (let i = 0; i < 8; i += 1) {
          spawnPacket(intakePackets, 2100, 3200, 1.5, 2.6);
          intakePackets[intakePackets.length - 1].t = rand(0, intakePackets[intakePackets.length - 1].duration);
        }
        for (let i = 0; i < 5; i += 1) {
          spawnPacket(supportPackets, 2000, 3000, 1.4, 2.4);
          supportPackets[supportPackets.length - 1].t = rand(0, supportPackets[supportPackets.length - 1].duration);
        }
        for (let i = 0; i < 4; i += 1) {
          spawnPacket(carePackets, 2500, 3600, 1.7, 2.8);
          carePackets[carePackets.length - 1].t = rand(0, carePackets[carePackets.length - 1].duration);
        }
      };

      const drawPulse = (x, y, color, radius, alpha) => {
        const glow = ctx.createRadialGradient(x, y, radius * 0.5, x, y, radius * 3.2);
        glow.addColorStop(0, toRgba(color, alpha));
        glow.addColorStop(1, toRgba(color, 0));
        ctx.fillStyle = glow;
        ctx.beginPath();
        ctx.arc(x, y, radius * 3.2, 0, Math.PI * 2);
        ctx.fill();

        ctx.fillStyle = toRgba(color, Math.min(0.85, alpha + 0.2));
        ctx.beginPath();
        ctx.arc(x, y, radius, 0, Math.PI * 2);
        ctx.fill();
      };

      const drawNodes = () => {
        const nodes = [
          { x: geometry.xPatient, y: geometry.yMid + 16, r: 8 },
          { x: geometry.xBot, y: geometry.yMid, r: 10 },
          { x: geometry.xClinician, y: geometry.yMid + 14, r: 8 }
        ];

        nodes.forEach((node, index) => {
          const ring = index === 1 ? palette.nodeSoft : palette.node;
          ctx.fillStyle = toRgba(ring, 0.26);
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.r + 5, 0, Math.PI * 2);
          ctx.fill();

          ctx.fillStyle = toRgba(ring, 0.56);
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.r, 0, Math.PI * 2);
          ctx.fill();
        });
      };

      const drawFlowPaths = () => {
        const wash = ctx.createRadialGradient(
          geometry.xBot,
          geometry.yMid,
          40,
          geometry.xBot,
          geometry.yMid,
          Math.max(width, height) * 0.72
        );
        wash.addColorStop(0, toRgba(palette.wash, 0.08));
        wash.addColorStop(1, "rgba(0,0,0,0)");
        ctx.fillStyle = wash;
        ctx.fillRect(0, 0, width, height);

        ctx.lineCap = "round";

        ctx.strokeStyle = toRgba(palette.laneSoft, 0.24);
        ctx.lineWidth = 14;
        ctx.beginPath();
        drawPath(geometry.patientToBot);
        drawPath(geometry.botToSupport);
        drawPath(geometry.botToClinician);
        ctx.stroke();

        ctx.lineWidth = 1.7;
        ctx.strokeStyle = toRgba(palette.lane, 0.36);
        ctx.beginPath();
        drawPath(geometry.patientToBot);
        drawPath(geometry.botToSupport);
        drawPath(geometry.botToClinician);
        ctx.stroke();

        ctx.setLineDash([5, 7]);
        ctx.lineWidth = 1.5;
        ctx.strokeStyle = toRgba(palette.alert, 0.3);
        ctx.beginPath();
        drawPath(geometry.alertPath);
        ctx.stroke();
        ctx.setLineDash([]);

        drawArrowHead(geometry.patientToBot, palette.lane, 0.28);
        drawArrowHead(geometry.botToSupport, palette.lane, 0.24);
        drawArrowHead(geometry.botToClinician, palette.lane, 0.28);
        drawArrowHead(geometry.alertPath, palette.alert, 0.3);

        drawNodes();
      };

      const drawHeartbeat = (time) => {
        const startX = width * 0.08;
        const endX = width * 0.92;
        const y = geometry.monitorY;
        const beatLength = 148;
        const drift = (time * 0.11) % beatLength;

        ctx.strokeStyle = toRgba(palette.monitorSoft, 0.32);
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.moveTo(startX, y);
        ctx.lineTo(endX, y);
        ctx.stroke();

        ctx.strokeStyle = toRgba(palette.monitor, 0.48);
        ctx.lineWidth = 1.8;
        ctx.beginPath();

        for (let x = startX; x <= endX; x += 2) {
          const local = (x + drift) % beatLength;
          let dy = Math.sin((x + time * 0.05) * 0.035) * height * 0.0022;

          if (local > 56 && local < 62) {
            dy -= (local - 56) * height * 0.008;
          } else if (local >= 62 && local < 68) {
            dy += (local - 62) * height * 0.01 - height * 0.048;
          } else if (local >= 68 && local < 78) {
            dy += height * 0.02 - (local - 68) * height * 0.003;
          }

          const yy = y + dy;
          if (x === startX) {
            ctx.moveTo(x, yy);
          } else {
            ctx.lineTo(x, yy);
          }
        }

        ctx.stroke();

        const tracerX = startX + ((time * 0.16) % (endX - startX));
        drawPulse(tracerX, y, palette.monitor, 2.1, 0.3);
      };

      const updatePackets = (collection, dt) =>
        collection.filter((packet) => {
          packet.t += dt;
          return packet.t <= packet.duration;
        });

      const drawPacketFlow = (collection, path, color) => {
        collection.forEach((packet) => {
          const t = Math.min(1, packet.t / packet.duration);
          const point = quadraticPoint(path, t);
          drawPulse(point.x, point.y, color, packet.radius, packet.alpha);
        });
      };

      const drawAlertSignals = () => {
        alertSignals.forEach((signal) => {
          const t = Math.min(1, signal.t / signal.duration);
          const point = quadraticPoint(geometry.alertPath, t);
          drawPulse(point.x, point.y, palette.alert, signal.radius + t * 0.8, signal.alpha * (1 - t * 0.42));
        });
      };

      const step = (dt) => {
        timers.intake += dt;
        timers.support += dt;
        timers.care += dt;
        timers.alert += dt;

        if (timers.intake > 340) {
          spawnPacket(intakePackets, 2100, 3200, 1.5, 2.6);
          timers.intake = 0;
        }
        if (timers.support > 1260) {
          spawnPacket(supportPackets, 2000, 3000, 1.4, 2.4);
          timers.support = 0;
        }
        if (timers.care > 1680) {
          spawnPacket(carePackets, 2500, 3600, 1.7, 2.8);
          timers.care = 0;
        }
        if (timers.alert > rand(5200, 7600)) {
          spawnPacket(alertSignals, 820, 1220, 2.3, 3.4);
          timers.alert = 0;
        }

        intakePackets = updatePackets(intakePackets, dt);
        supportPackets = updatePackets(supportPackets, dt);
        carePackets = updatePackets(carePackets, dt);
        alertSignals = updatePackets(alertSignals, dt);
      };

      const drawFrame = (time) => {
        ctx.clearRect(0, 0, width, height);
        drawFlowPaths();
        drawPacketFlow(intakePackets, geometry.patientToBot, palette.intake);
        drawPacketFlow(supportPackets, geometry.botToSupport, palette.support);
        drawPacketFlow(carePackets, geometry.botToClinician, palette.care);
        drawAlertSignals();
        drawHeartbeat(time);
      };

      const renderStaticFrame = () => {
        drawFrame(timeline);
      };

      const animate = (timestamp) => {
        if (!lastFrame) {
          lastFrame = timestamp;
        }
        const dt = Math.min(80, timestamp - lastFrame);
        lastFrame = timestamp;
        timeline += dt;

        step(dt);
        drawFrame(timeline);
        animationId = window.requestAnimationFrame(animate);
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
        seedScene();
        if (prefersReducedMotion.matches) {
          renderStaticFrame();
          return;
        }
        animationId = window.requestAnimationFrame(animate);
      };

      const onThemeMaybeChanged = () => {
        updatePalette();
        drawFrame(timeline);
      };

      const onVisibilityChange = () => {
        if (document.hidden) {
          stop();
          return;
        }
        start();
      };

      updatePalette();
      resize();
      start();

      window.addEventListener("resize", () => {
        resize();
        drawFrame(timeline);
      });
      prefersReducedMotion.addEventListener("change", start);
      document.addEventListener("visibilitychange", onVisibilityChange);

      const observer = new MutationObserver(onThemeMaybeChanged);
      observer.observe(root, { attributes: true, attributeFilter: ["data-theme", "style", "class"] });
    })();
  </script>
</div>
