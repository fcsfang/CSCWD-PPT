<template>
  <div class="sim-gap">
    <section class="domain-panel source-panel">
      <h3>Source Domain</h3>
      <div class="keyword-list source-keywords">
        <span>clean</span>
        <span>labeled</span>
        <span>controlled</span>
      </div>

      <svg class="asset-sketch" viewBox="0 0 300 120" aria-label="controlled test rig">
        <path class="soft-fill" d="M28 76 H91 V99 H28 Z" />
        <circle class="outline" cx="100" cy="76" r="36" />
        <circle class="outline light" cx="100" cy="76" r="14" />
        <path class="outline" d="M136 54 H238 V99 H136 Z" />
        <path class="soft-fill" d="M238 76 H286 V99 H238 Z" />
        <path class="outline" d="M28 99 H286" />
      </svg>
      <div class="asset-caption">
        <span>controlled test rig</span>
      </div>
      <svg class="wave clean-wave" viewBox="0 0 300 52" aria-label="clean vibration waveform">
        <path class="axis" d="M16 42 H286" />
        <path class="wave-line" d="M18 30 L38 26 L55 29 L72 25 L90 31 L106 7 L123 32 L144 29 L160 26 L178 28 L194 25 L211 26 L229 12 L246 31 L264 28 L286 27" />
      </svg>
    </section>

    <div class="arrow source-arrow" aria-hidden="true"></div>

    <section class="shift-panel">
      <h3>Distribution Shift</h3>
      <div class="shift-formula">P(X<sub>s</sub>) ≠ P(X<sub>t</sub>)</div>
      <svg class="distribution-plot" viewBox="0 0 360 210" aria-label="source and target distribution shift">
        <path class="plot-border" d="M26 24 H336 V184 H26 Z" />
        <path class="axis" d="M58 154 H304" />
        <path class="axis" d="M58 154 V55" />
        <text class="source-label" x="112" y="47">source</text>
        <text class="target-label" x="214" y="47">target</text>
        <path class="source-curve" d="M62 151 C86 150, 96 126, 112 99 C132 64, 155 58, 174 78 C193 98, 199 133, 226 145 C242 152, 261 153, 286 151" />
        <path class="target-curve" d="M76 151 C103 149, 127 138, 148 117 C174 91, 202 78, 228 89 C254 100, 270 128, 299 149" />
        <circle class="source-dot" cx="139" cy="83" r="5" />
        <circle class="target-dot" cx="235" cy="92" r="5" />
      </svg>
    </section>

    <div class="arrow target-arrow" aria-hidden="true"></div>

    <section class="domain-panel target-panel">
      <h3>Target Domain</h3>
      <div class="keyword-list target-keywords">
        <span>noisy</span>
        <span>unlabeled</span>
        <span>variable-speed</span>
      </div>

      <svg class="asset-sketch train-sketch" viewBox="0 0 300 120" aria-label="high-speed train asset">
        <path class="train-body" d="M38 84 L54 42 C70 26 104 22 202 22 C244 22 266 35 278 61 L260 98 H50 Z" />
        <path class="window" d="M88 47 H128 V68 H88 Z" />
        <path class="window" d="M146 47 H186 V68 H146 Z" />
        <path class="window" d="M204 47 H244 V68 H204 Z" />
        <circle class="wheel" cx="104" cy="103" r="13" />
        <circle class="wheel" cx="238" cy="103" r="13" />
      </svg>
      <div class="asset-caption">
        <span>real train edge data</span>
      </div>
      <svg class="wave noisy-wave" viewBox="0 0 300 52" aria-label="noisy vibration waveform">
        <path class="axis" d="M16 44 H286" />
        <path class="wave-line" d="M18 30 L27 15 L35 35 L46 9 L55 27 L64 14 L72 40 L82 25 L92 34 L103 4 L113 43 L126 16 L139 35 L150 14 L164 37 L172 4 L181 42 L197 20 L207 36 L219 13 L229 40 L243 22 L252 37 L260 25 L270 39 L286 16" />
      </svg>
    </section>
  </div>
</template>

<style scoped>
.sim-gap {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 34px minmax(0, 1.05fr) 34px minmax(0, 1fr);
  gap: 12px;
  align-items: center;
}

.domain-panel,
.shift-panel {
  min-height: 312px;
  border: 1px solid var(--border);
  border-radius: 6px;
  background: #fff;
  padding: 13px 16px 11px;
}

.source-panel {
  border-color: color-mix(in srgb, var(--primary) 76%, var(--border));
}

.target-panel {
  border-color: color-mix(in srgb, var(--accent) 76%, var(--border));
}

h3 {
  margin: 0;
  font-size: 1.05rem;
  line-height: 1.18;
  font-weight: 700;
}

.source-panel h3 {
  color: var(--primary);
}

.target-panel h3 {
  color: var(--accent);
}

.source-status {
  color: #007A3D;
  font-weight: 800;
}

.target-status {
  color: #C2410C;
  font-weight: 800;
}

.keyword-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 7px;
  margin-top: 14px;
}

.keyword-list span {
  border: 1px solid var(--border);
  border-radius: 4px;
  background: #fff;
  padding: 6px 4px;
  text-align: center;
  font-size: .76rem;
  font-weight: 720;
}

.source-keywords span {
  color: #007A3D;
  border-color: color-mix(in srgb, #007A3D 42%, var(--border));
}

.target-keywords span {
  color: #C2410C;
  border-color: color-mix(in srgb, #C2410C 42%, var(--border));
}

.asset-sketch {
  display: block;
  width: 100%;
  height: 88px;
  margin-top: 24px;
}

.outline,
.train-body {
  fill: none;
  stroke: currentColor;
  stroke-width: 3;
}

.source-panel .asset-sketch {
  color: var(--primary);
}

.target-panel .asset-sketch {
  color: var(--accent);
}

.soft-fill,
.window {
  fill: color-mix(in srgb, currentColor 8%, #fff);
  stroke: currentColor;
  stroke-width: 2;
}

.outline.light,
.wheel {
  fill: #fff;
  stroke: currentColor;
  stroke-width: 3;
}

.asset-caption {
  display: grid;
  gap: 3px;
  margin-top: 0;
  text-align: center;
  color: var(--muted);
  font-size: .74rem;
  line-height: 1.2;
}

.wave {
  display: block;
  width: 100%;
  height: 42px;
  margin-top: 9px;
}

.axis {
  fill: none;
  stroke: #A7B0BE;
  stroke-width: 1.5;
}

.wave-line {
  fill: none;
  stroke: currentColor;
  stroke-width: 2.6;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.clean-wave {
  color: var(--primary);
}

.noisy-wave {
  color: var(--accent);
}

.arrow {
  height: 1px;
  background: var(--text);
  opacity: .78;
  position: relative;
}

.arrow::after {
  content: "";
  position: absolute;
  right: -1px;
  top: -7px;
  border-left: 13px solid var(--text);
  border-top: 7px solid transparent;
  border-bottom: 7px solid transparent;
}

.target-arrow,
.target-arrow::after {
  color: var(--accent);
}

.target-arrow {
  background: var(--accent);
}

.target-arrow::after {
  border-left-color: var(--accent);
}

.shift-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

.shift-panel h3 {
  font-size: 1.1rem;
}

.shift-formula {
  margin-top: 16px;
  color: var(--text);
  font-family: "Times New Roman", Times, serif;
  font-size: 2.12rem;
  font-weight: 600;
}

.distribution-plot {
  width: 100%;
  height: 168px;
  margin-top: 12px;
}

.plot-border {
  fill: none;
  stroke: var(--border);
  stroke-width: 1.4;
}

.source-label,
.target-label {
  font-family: Inter, Arial, Helvetica, sans-serif;
  font-size: 13px;
  font-weight: 650;
}

.source-label {
  fill: var(--primary);
}

.target-label {
  fill: var(--accent);
}

.source-curve,
.target-curve {
  fill: none;
  stroke-width: 3;
  stroke-dasharray: 8 7;
  stroke-linecap: round;
}

.source-curve {
  stroke: var(--primary);
}

.target-curve {
  stroke: var(--accent);
}

.source-dot {
  fill: var(--primary);
}

.target-dot {
  fill: var(--accent);
}
</style>
