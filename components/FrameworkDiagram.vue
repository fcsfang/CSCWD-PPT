<template>
  <div class="framework">
    <div class="pipeline">
      <div class="signals">
        <div class="signal source">
          <span class="label-main">Source signals</span>
          <span>labeled laboratory data</span>
        </div>
        <div class="signal target">
          <span class="label-main">Target signals</span>
          <span>unlabeled train data</span>
        </div>
      </div>
      <div class="edge"></div>
      <div class="node physics">
        <span class="label-main">Frozen Φ<sub>phy</sub></span>
        <span>hard-wired physics prior</span>
      </div>
      <div class="edge"></div>
      <div class="node">
        <span class="label-main">Mechanism-aligned features</span>
        <span>physics-consistent representation</span>
      </div>
      <div class="edge"></div>
      <div class="node final">
        <span class="label-main">DANN alignment + fault prediction</span>
        <span>domain-invariant diagnosis</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.framework {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--card);
  padding: 24px 26px;
}
.pipeline {
  display: grid;
  grid-template-columns: 1.18fr 44px 1fr 44px 1.2fr 44px 1.24fr;
  align-items: center;
}
.signals {
  display: grid;
  gap: 10px;
}
.signal,
.node {
  border: 1px solid var(--border);
  border-radius: 4px;
  background: #fff;
  color: var(--text);
  min-height: 62px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-weight: 640;
  font-size: .9rem;
}
.signal span,
.node span {
  color: var(--muted);
  font-size: .68rem;
  font-weight: 500;
  margin-top: 3px;
}
.signal .label-main,
.node .label-main {
  color: var(--text);
  font-size: .9rem;
  font-weight: 650;
  margin-top: 0;
}
.source {
  border-top: 2px solid var(--primary);
}
.target,
.final {
  border-top: 2px solid var(--accent);
}
.physics {
  border-top: 2px solid var(--accent);
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
</style>
