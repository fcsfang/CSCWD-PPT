<template>
  <div class="evidence">
    <figure>
      <img :src="left" :alt="leftTitle" />
      <figcaption>{{ leftTitle }}</figcaption>
    </figure>
    <figure>
      <img :src="right" :alt="rightTitle" />
      <figcaption>{{ rightTitle }}</figcaption>
    </figure>
  </div>
</template>

<script setup>
defineProps({
  left: { type: String, required: true },
  right: { type: String, required: true },
  leftTitle: { type: String, required: true },
  rightTitle: { type: String, required: true },
})
</script>

<style scoped>
.evidence {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}
figure {
  margin: 0;
}
img {
  width: 100%;
  height: 286px;
  object-fit: contain;
  border: 1px solid var(--border);
  background: #fff;
  padding: 6px;
}
figcaption {
  color: var(--text);
  margin-top: 7px;
  font-size: .78rem;
  font-weight: 600;
}
</style>
