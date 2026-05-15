<script setup>
import katex from 'katex'
import 'katex/dist/katex.min.css'

const items = [
  {
    title: 'Source domain',
    tex: String.raw`D_s=\{(x_i^s,y_i^s)\}_{i=1}^{n_s}`,
  },
  {
    title: 'Target domain',
    tex: String.raw`D_t=\{x_j^t\}_{j=1}^{n_t}`,
  },
  {
    title: 'Domain shift',
    tex: String.raw`P(X_s)\neq P(X_t)`,
  },
  {
    title: 'Learning objective',
    tex: String.raw`f^\star=\arg\min_f \mathcal{R}_t(f)`,
  },
].map(item => ({
  ...item,
  html: katex.renderToString(item.tex, {
    displayMode: true,
    throwOnError: false,
    strict: 'ignore',
  }),
}))
</script>

<template>
  <div class="problem-setting">
    <div v-for="item in items" :key="item.title" class="problem-card">
      <div class="problem-title">{{ item.title }}</div>
      <div class="problem-formula" v-html="item.html"></div>
    </div>
  </div>
</template>

<style scoped>
.problem-setting {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  margin-top: 22px;
}

.problem-card {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: #fff;
  min-height: 126px;
  padding: 17px 20px;
}

.problem-title {
  color: var(--primary);
  font-size: .9rem;
  font-weight: 720;
  text-transform: uppercase;
}

.problem-formula {
  margin-top: 14px;
  color: var(--text);
}

.problem-formula :deep(.katex-display) {
  margin: 0;
}

.problem-formula :deep(.katex) {
  font-size: 1.42rem;
}
</style>
