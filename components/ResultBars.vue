<template>
  <div class="bars">
    <div class="bar-head">
      <span>Method</span>
      <span>Target accuracy</span>
      <span>F1</span>
    </div>
    <div v-for="row in rows" :key="row.name" class="bar-row">
      <div class="name">{{ row.name }}</div>
      <div class="track">
        <div class="fill" :class="{ ours: row.ours }" :style="{ width: row.acc + '%' }"></div>
        <span v-if="row.ours" class="delta">+28.14 pp vs ResNet-18</span>
      </div>
      <div class="value">{{ row.acc.toFixed(2) }}%</div>
      <div class="f1">{{ row.f1 }}</div>
    </div>
  </div>
</template>

<script setup>
const rows = [
  { name: 'SVM', acc: 42.15, f1: '0.387' },
  { name: 'Random Forest', acc: 48.62, f1: '0.453' },
  { name: 'CNN', acc: 61.30, f1: '0.589' },
  { name: 'ResNet-18', acc: 65.80, f1: '0.621' },
  { name: 'MDC-DAN', acc: 93.94, f1: '0.942', ours: true },
]
</script>

<style scoped>
.bars {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--card);
  padding: 18px 20px;
}
.bar-head {
  display: grid;
  grid-template-columns: 138px 1fr 54px;
  gap: 14px;
  color: var(--muted);
  font-size: .7rem;
  font-weight: 650;
  text-transform: uppercase;
  margin-bottom: 12px;
}
.bar-row {
  display: grid;
  grid-template-columns: 138px 1fr 78px 54px;
  gap: 14px;
  align-items: center;
  margin-bottom: 13px;
  color: var(--text);
  font-size: .88rem;
}
.bar-row:last-child {
  margin-bottom: 0;
}
.track {
  height: 20px;
  background: #EFF2F5;
  position: relative;
  border: 1px solid #E4E8EF;
}
.fill {
  height: 100%;
  background: #AEB7C2;
}
.fill.ours {
  background: var(--primary);
}
.delta {
  position: absolute;
  left: min(68%, calc(93.94% + 8px));
  top: 50%;
  transform: translateY(-50%);
  color: var(--accent);
  font-size: .74rem;
  font-weight: 700;
  white-space: nowrap;
}
.value {
  color: var(--text);
  font-weight: 650;
}
.f1 {
  color: var(--muted);
  font-size: .78rem;
}
</style>
