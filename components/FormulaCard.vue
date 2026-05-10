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
  padding: 14px 16px;
  min-height: 126px;
}
.title {
  color: var(--rust);
  font-weight: 700;
  font-size: .78rem;
  text-transform: uppercase;
  letter-spacing: .03em;
}
.formula {
  margin-top: 12px;
  color: var(--ink);
  font-family: "Times New Roman", "STIX Two Text", serif;
  font-size: 1.2rem;
  line-height: 1.25;
}
p {
  margin: 10px 0 0;
  color: var(--muted);
  font-size: .75rem;
}
</style>
