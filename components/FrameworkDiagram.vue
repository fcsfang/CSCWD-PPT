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
        <span class="label-main">h<sub>phy</sub> ∈ R<sup>15</sup></span>
        <span>mechanism-aligned features</span>
      </div>
      <div class="edge"></div>
      <div class="node">
        <span class="label-main">G<sub>f</sub></span>
        <span>feature extractor</span>
      </div>
      <div class="edge"></div>
      <div class="node latent">
        <span class="label-main">z</span>
        <span>latent representation</span>
      </div>
    </div>

    <div class="branch-area">
      <div class="branch-connector" aria-hidden="true"></div>
      <div class="branch">
        <div class="stem"></div>
        <div class="node head label">
          <span class="label-main">G<sub>y</sub></span>
          <span>fault prediction</span>
        </div>
      </div>
      <div class="branch adversarial">
        <div class="stem"></div>
        <div class="node head">
          <span class="label-main">GRL → G<sub>d</sub></span>
          <span>domain alignment</span>
        </div>
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
  grid-template-columns: 1.14fr 34px .98fr 34px .96fr 34px .82fr 34px .82fr;
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
.latent,
.adversarial .head {
  border-top: 2px solid var(--accent);
}
.latent {
  position: relative;
}
.latent::after {
  content: "";
  position: absolute;
  left: 50%;
  top: 100%;
  width: 1px;
  height: 36px;
  background: var(--border);
  transform: translateX(-50%);
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
.branch-area {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  align-items: start;
  margin-top: 24px;
  padding-top: 42px;
  width: 38%;
  margin-left: auto;
}
.branch-connector {
  position: absolute;
  left: 0;
  right: 0;
  top: -24px;
  height: 66px;
  pointer-events: none;
}
.branch-connector::before {
  content: "";
  position: absolute;
  left: 75%;
  top: 0;
  width: 1px;
  height: 45px;
  background: var(--border);
}
.branch-connector::after {
  content: "";
  position: absolute;
  left: 25%;
  right: 25%;
  top: 45px;
  height: 1px;
  background: var(--border);
}
.branch {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.stem {
  position: absolute;
  top: -21px;
  width: 1px;
  height: 21px;
  background: var(--border);
}
.head {
  width: 100%;
  min-height: 56px;
  margin-top: 0;
}
.label {
  border-top: 2px solid var(--primary);
}
</style>
