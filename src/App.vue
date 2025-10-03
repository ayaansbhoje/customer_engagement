<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import CustomerList from './components/CustomerList.vue';
import CustomerDetail from './components/CustomerDetail.vue';
import EngagementForm from './components/EngagementForm.vue';

// Holds the array of customers fetched from the API
const customers = ref([]);
// Holds the single customer object that the user clicks on
const selectedCustomer = ref(null);
// A boolean to show a loading message while fetching data
const isLoading = ref(true);

// This is a lifecycle hook that runs once when the component is created
onMounted(async () => {
  try {
    // Fetch user data from the API
    const response = await axios.get('https://jsonplaceholder.typicode.com/users');
    customers.value = response.data;
  } catch (error) {
    console.error("Failed to fetch customers:", error);
  } finally {
    // Hide the loading message once the request is complete
    isLoading.value = false;
  }
});

// This function is triggered by an event from the CustomerList component
function handleCustomerSelected(customer) {
  selectedCustomer.value = customer;
}
</script>

<template>
  <div id="app-wrapper">
    <header>
      <h1>Customer Engagement</h1>
    </header>
    <main>
      <CustomerList
        :customers="customers"
        :is-loading="isLoading"
        :selected-customer="selectedCustomer"
        @customer-selected="handleCustomerSelected"
      />

      <div class="details-and-form" v-if="selectedCustomer">
        <CustomerDetail :customer="selectedCustomer" />
        <EngagementForm :customer="selectedCustomer" />
      </div>

      <div class="placeholder-card" v-else>
        <p>Please select a customer from the list to see their details and send a message.</p>
      </div>
    </main>
  </div>
</template>

<style>
/* Define a modern color palette and font using CSS variables */
:root {
  --primary-color: #42b883; /* Vue Green */
  --primary-color-dark: #3aa875;
  --bg-color: #f2f4f7;
  --card-bg-color: #ffffff;
  --text-color: #333;
  --text-color-light: #666;
  --border-color: #e0e0e0;
  --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
    Arial, sans-serif;
}

/* Basic CSS Reset */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* MODIFICATION 1: Center everything by making the body a flex container */
body {
  font-family: var(--font-family);
  background-color: var(--bg-color);
  color: var(--text-color);
  
  /* --- ADD THESE LINES --- */
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  /* ----------------------- */
}

/* MODIFICATION 2: Remove the margin that was previously used for centering */
#app-wrapper {
  max-width: 1000px;
  padding-left: 20rem;
  width: 100%;
  /* --- ADD/MODIFY THIS LINE --- */
  margin: 6px auto; /* This centers it horizontally and adds 2rem space top/bottom */
  /* Or if you only want it to move slightly right and not fully center: */
  /* margin-left: 5%; */ /* Example: moves it 5% from the left edge */
}
header h1 {
  font-size: 2rem;
  font-weight: 600;
  padding-bottom: 1rem;
  border-bottom: 1px solid var(--border-color);
  margin-bottom: 2rem;
  text-align: center;
}

main {
  display: flex;
  gap: 2rem;
  align-items: flex-start; /* Align items to the top */
}

.details-and-form {
  flex: 1; /* Allow this column to take remaining space */
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

/* A reusable card style for our components */
.card {
  background-color: var(--card-bg-color);
  border-radius: 8px;
  border: 1px solid var(--border-color);
  padding: 1.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

/* Style for the placeholder when no customer is selected */
.placeholder-card {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 300px;
  background-color: var(--card-bg-color);
  border-radius: 8px;
  border: 2px dashed var(--border-color);
  color: var(--text-color-light);
  padding: 2rem;
  text-align: center;
}
</style>