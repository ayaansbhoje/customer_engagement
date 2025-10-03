<script setup>
import { ref } from 'vue';
const props = defineProps({
  customer: Object,
});
const message = ref('');
function handleSubmit() {
  if (!message.value) {
    alert('Please enter a message.');
    return;
  }
  console.log(`Sending message to ${props.customer.name}: "${message.value}"`);
  alert(`Message sent to ${props.customer.name}!`);
  message.value = '';
}
</script>

<template>
  <div class="card">
    <h3>Send Message to {{ customer.name }}</h3>
    <form @submit.prevent="handleSubmit">
      <textarea
        v-model="message"
        placeholder="Type your engagement message..."
      ></textarea>
      <button type="submit">Send Message</button>
    </form>
  </div>
</template>

<style scoped>
h3 {
  margin-bottom: 1rem;
  font-weight: 600;
}

textarea {
  width: 100%;
  height: 120px;
  padding: 0.75rem;
  border-radius: 6px;
  border: 1px solid var(--border-color);
  font-family: var(--font-family);
  font-size: 1rem;
  resize: vertical;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

textarea:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(66, 184, 131, 0.2);
}

button {
  display: block;
  width: 100%;
  padding: 0.8rem;
  margin-top: 1rem;
  background-color: var(--primary-color);
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

button:hover {
  background-color: var(--primary-color-dark);
  transform: translateY(-2px);
}
</style>