<template>
  <div class="bars result-bars">
    <div class="bar-head">
      <span>Method</span>
      <span>Target accuracy</span>
    </div>
    <div v-for="row in rows" :key="row.name" class="bar-row">
      <div class="name">{{ row.name }}</div>
      <div class="track">
        <div class="fill" :class="{ ours: row.ours }" :style="{ width: row.acc + '%' }"></div>
      </div>
      <div class="value">{{ row.acc.toFixed(2) }}%</div>
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
  grid-template-columns: 128px 1fr 70px;
  gap: 14px;
  color: var(--muted);
  font-size: .7rem;
  font-weight: 650;
  text-transform: uppercase;
  margin-bottom: 12px;
}
.bar-row {
  display: grid;
  grid-template-columns: 128px 1fr 70px;
  gap: 14px;
  align-items: center;
  margin-bottom: 16px;
  color: var(--text);
  font-size: .88rem;
}
.bar-row:last-child {
  margin-bottom: 0;
}
.track {
  height: 22px;
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
.value {
  color: var(--text);
  font-weight: 650;
}
</style>
