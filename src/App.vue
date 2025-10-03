<script setup>
import CustomerList from './components/CustomerList.vue';
import CustomerDetail from './components/CustomerDetail.vue';
import EngagementForm from './components/EngagementForm.vue';
</script>

<template>
  <div id="app-wrapper">
    <header>
      <h1>Customer Engagement</h1>
    </header>
    <main>
      <CustomerList />
      <div class="details-and-form">
        <CustomerDetail />
        <EngagementForm />
      </div>
    </main>
  </div>
</template>

<style>
#app-wrapper { max-width: 900px; margin: 2rem auto; font-family: sans-serif; }
header { border-bottom: 1px solid #ddd; padding-bottom: 1rem; }
main { display: flex; gap: 2rem; margin-top: 1rem; }
.details-and-form { flex-grow: 1; display: flex; flex-direction: column; gap: 1.5rem;}
</style>