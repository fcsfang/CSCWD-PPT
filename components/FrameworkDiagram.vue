<template>
  <div class="framework">
    <div class="row">
      <div class="domain source">
        <span class="label-main">Source signal x<sup>s</sup></span>
        <span>labeled CWRU samples</span>
      </div>
      <div class="domain target">
        <span class="label-main">Target signal x<sup>t</sup></span>
        <span>unlabeled train samples</span>
      </div>
    </div>

    <div v-click="1" class="connector physics-step"></div>

    <div class="pipeline">
      <div v-click="1" class="node physics physics-step">
        <span class="label-main">Φ<sub>phy</sub></span>
        <span>frozen physics encoding</span>
      </div>
      <div v-click="1" class="edge physics-step"></div>
      <div v-click="1" class="node physics-step">
        <span class="label-main">h<sub>phy</sub></span>
        <span>15-D mechanism feature</span>
      </div>
      <div v-click="2" class="edge adaptation-step"></div>
      <div v-click="2" class="node adaptation-step">
        <span class="label-main">G<sub>f</sub></span>
        <span>feature extractor</span>
      </div>
      <div v-click="2" class="edge adaptation-step"></div>
      <div v-click="2" class="node adaptation-step">
        <span class="label-main">z</span>
        <span>latent representation</span>
      </div>
    </div>

    <div v-click="2" class="branches adaptation-step">
      <div class="branch">
        <div class="node small">
          <span class="label-main">G<sub>y</sub></span>
          <span>fault classifier</span>
        </div>
        <p>L<sub>y</sub> on source labels</p>
      </div>
      <div class="branch adversarial">
        <div class="node small">
          <span class="label-main">GRL → G<sub>d</sub></span>
          <span>domain discriminator</span>
        </div>
        <p>domain confusion for source / target</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.framework {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--card);
  padding: 18px 22px 16px;
}
.row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}
.domain,
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
.domain span,
.node span {
  color: var(--muted);
  font-size: .68rem;
  font-weight: 500;
  margin-top: 3px;
}
.domain .label-main,
.node .label-main {
  color: var(--text);
  font-size: .94rem;
  font-weight: 650;
  margin-top: 0;
}
.source {
  border-top: 2px solid var(--primary);
}
.target,
.adversarial .node {
  border-top: 2px solid var(--accent);
}
.connector {
  width: 1px;
  height: 22px;
  background: var(--border);
  margin: 0 auto;
}
.pipeline {
  display: grid;
  grid-template-columns: 1.1fr 34px 1.1fr 34px 1.1fr 34px 1.1fr;
  align-items: center;
}
.physics {
  border-top: 2px solid var(--accent);
}
.physics-step {
  --slidev-click-transition: opacity 180ms ease;
}
.adaptation-step {
  --slidev-click-transition: opacity 180ms ease;
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
.branches {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
  margin-top: 18px;
  width: 48%;
  margin-left: auto;
}
.branch {
  border-top: 1px solid var(--border);
  padding-top: 12px;
}
.node.small {
  min-height: 58px;
}
.branch p {
  margin: 6px 0 0;
  color: var(--muted);
  font-size: .68rem;
  text-align: center;
}
</style>
