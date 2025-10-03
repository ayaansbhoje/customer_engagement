<script setup>
defineProps({
  customers: Array,
  isLoading: Boolean,
  selectedCustomer: Object, // To know which customer is active
});
const emit = defineEmits(['customer-selected']);
</script>

<template>
  <div class="list-container">
    <h2>Customers</h2>
    <div v-if="isLoading" class="loading">Loading...</div>
    <ul v-else>
      <li
        v-for="customer in customers"
        :key="customer.id"
        :class="{ active: selectedCustomer && selectedCustomer.id === customer.id }"
        @click="emit('customer-selected', customer)"
      >
        {{ customer.name }}
        <small>{{ customer.company.name }}</small>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.list-container {
  width: 320px;
  flex-shrink: 0; /* Prevent the list from shrinking */
  background-color: var(--card-bg-color);
  border-radius: 8px;
  border: 1px solid var(--border-color);
  padding: 1rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

h2 {
  margin-bottom: 1rem;
  font-weight: 600;
}

.loading {
  color: var(--text-color-light);
}

ul {
  list-style: none;
  padding: 0;
  max-height: 60vh; /* Make the list scrollable if it's too long */
  overflow-y: auto;
}

li {
  display: flex;
  flex-direction: column;
  padding: 0.75rem 1rem;
  cursor: pointer;
  border-radius: 6px;
  border: 1px solid transparent;
  transition: background-color 0.2s ease, border-color 0.2s ease;
}

li small {
  color: var(--text-color-light);
  font-size: 0.8rem;
}

li:hover {
  background-color: var(--bg-color);
}

li.active {
  background-color: #e8f5e9; /* A light green for the active state */
  border-color: var(--primary-color);
  font-weight: 600;
}
</style>