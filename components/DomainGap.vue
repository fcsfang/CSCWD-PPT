<template>
  <div class="gap-card">
    <div class="domain source">
      <div class="label">Source Domain</div>
      <div class="sub">CWRU laboratory data · labeled</div>
      <svg viewBox="0 0 360 110" aria-label="source distribution">
        <path class="axis" d="M20 88 H338" />
        <path class="curve source-curve" d="M30 82 C70 78, 82 36, 115 35 C145 34, 151 82, 188 77 C218 72, 230 42, 262 45 C298 49, 304 78, 336 74" />
        <circle cx="115" cy="35" r="5" />
        <circle cx="262" cy="45" r="5" />
      </svg>
    </div>
    <div class="bridge">
      <span>Sim-to-Real gap</span>
      <div class="arrow">→</div>
      <p>P(X<sub>s</sub>) ≠ P(X<sub>t</sub>)</p>
    </div>
    <div class="domain target">
      <div class="label">Target Domain</div>
      <div class="sub">High-speed train data · unlabeled</div>
      <svg viewBox="0 0 360 110" aria-label="target distribution">
        <path class="axis" d="M20 88 H338" />
        <path class="curve target-curve" d="M28 72 C58 82, 86 53, 116 63 C148 74, 163 23, 201 30 C246 38, 242 78, 278 76 C312 75, 318 42, 340 49" />
        <circle cx="201" cy="30" r="5" />
        <circle cx="116" cy="63" r="5" />
      </svg>
    </div>
  </div>
</template>

<style scoped>
.gap-card {
  display: grid;
  grid-template-columns: 1fr 150px 1fr;
  gap: 16px;
  align-items: center;
}
.domain {
  border: 1px solid var(--line);
  border-radius: 4px;
  background: #fff;
  padding: 16px;
}
.label {
  color: var(--ink);
  font-weight: 760;
  font-size: 1rem;
}
.sub {
  color: var(--muted);
  font-size: .75rem;
  margin-top: 3px;
}
svg {
  width: 100%;
  margin-top: 10px;
}
.axis {
  stroke: var(--border);
  stroke-width: 1.5;
}
.curve {
  fill: none;
  stroke-width: 3;
  stroke-linecap: round;
}
.source-curve {
  stroke: var(--navy);
}
.target-curve {
  stroke: var(--rust);
}
circle {
  fill: var(--accent);
}
.bridge {
  text-align: center;
  color: var(--muted);
}
.bridge span {
  color: var(--rust);
  font-size: .78rem;
  text-transform: uppercase;
  letter-spacing: .03em;
  font-weight: 700;
}
.arrow {
  color: var(--ink);
  font-size: 1.8rem;
  line-height: 1;
}
.bridge p {
  font-family: "Times New Roman", serif;
  font-size: 1rem;
  margin: 4px 0 0;
}
</style>
