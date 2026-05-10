<template>
  <div class="formula-card">
    <div class="title">{{ title }}</div>
    <div class="formula"><slot /></div>
    <p v-if="note">{{ note }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: { type: String, required: true },
  note: { type: String, default: '' },
})
</script>

<style scoped>
.formula-card {
  border: 1px solid var(--line);
  border-radius: 6px;
  background: #fff;
  padding: 13px 16px;
  min-height: 104px;
}
.title {
  color: var(--primary);
  font-weight: 700;
  font-size: .82rem;
  text-transform: uppercase;
  letter-spacing: 0;
}
.formula {
  margin-top: 12px;
  color: var(--ink);
  font-family: "Times New Roman", "STIX Two Text", serif;
  font-size: 1.26rem;
  line-height: 1.25;
}
p {
  margin: 10px 0 0;
  color: var(--muted);
  font-size: .82rem;
}
</style>
