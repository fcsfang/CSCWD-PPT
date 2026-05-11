<template>
  <div class="custom-pagination">
    {{ $page }}
  </div>
</template>

<style scoped>
.custom-pagination {
  position: absolute;
  right: 18px;
  bottom: 14px;
  z-index: 40;
  color: rgba(20, 25, 34, 0.58);
  font-size: 12px;
  line-height: 1;
  font-variant-numeric: tabular-nums;
}
</style>
