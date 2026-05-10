<template>
  <div class="dann">
    <div class="main-line">
      <div class="node input">
        <span class="label-main">h<sub>phy</sub></span>
        <span>physics-aligned 15-D feature</span>
      </div>
      <div class="edge"></div>
      <div class="node">
        <span class="label-main">G<sub>f</sub></span>
        <span>15 → 64 → 32</span>
      </div>
      <div class="edge"></div>
      <div class="node latent">
        <span class="label-main">z</span>
        <span>latent fault feature</span>
      </div>
    </div>

    <div class="branch-line">
      <div></div>
      <div class="branch">
        <div class="stem"></div>
        <div class="head label">
          <span class="label-main">G<sub>y</sub></span>
          <span>32 → 16 → 4 · fault class</span>
        </div>
      </div>
      <div class="branch adversarial">
        <div class="stem"></div>
        <div class="head">
          <span class="label-main">GRL → G<sub>d</sub></span>
          <span>32 → 16 → 1 · source / target</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dann {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--card);
  padding: 20px 24px 18px;
}
.main-line {
  display: grid;
  grid-template-columns: 1fr 56px 1fr 56px 1fr;
  align-items: center;
}
.node,
.head {
  border: 1px solid var(--border);
  border-radius: 4px;
  min-height: 68px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: var(--text);
  font-weight: 650;
  background: #fff;
}
.input {
  border-top: 2px solid var(--accent);
}
.latent,
.label {
  border-top: 2px solid var(--primary);
}
.node span,
.head span {
  color: var(--muted);
  margin-top: 5px;
  font-size: .7rem;
  font-weight: 500;
}
.node .label-main,
.head .label-main {
  color: var(--text);
  font-size: 1rem;
  font-weight: 650;
  margin-top: 0;
}
.edge {
  height: 1px;
  background: var(--border);
  position: relative;
}
.edge::after {
  content: "";
  position: absolute;
  right: 0;
  top: -4px;
  border-left: 7px solid var(--border);
  border-top: 4px solid transparent;
  border-bottom: 4px solid transparent;
}
.branch-line {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 18px;
  margin-top: 14px;
}
.branch {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.stem {
  width: 1px;
  height: 24px;
  background: var(--border);
}
.head {
  width: 100%;
  min-height: 62px;
}
.adversarial .head {
  border-top: 2px solid var(--accent);
}
</style>
