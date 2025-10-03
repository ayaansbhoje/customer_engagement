<script setup>
defineProps({
  customer: Object,
});
</script>

<template>
  <div class="card">
    <h3>Details</h3>
    <div class="detail-item">
      <strong>Name:</strong>
      <span>{{ customer.name }}</span>
    </div>
    <div class="detail-item">
      <strong>Email:</strong>
      <span>{{ customer.email }}</span>
    </div>
    <div class="detail-item">
      <strong>Company:</strong>
      <span>{{ customer.company.name }}</span>
    </div>
  </div>
</template>

<style scoped>
h3 {
  margin-bottom: 1rem;
  font-weight: 600;
}
.detail-item {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0;
  border-bottom: 1px solid var(--bg-color);
}
.detail-item:last-child {
  border-bottom: none;
}
.detail-item span {
  color: var(--text-color-light);
  text-align: right;
}
</style>