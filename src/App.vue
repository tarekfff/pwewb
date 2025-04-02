<script setup>
import { ref, onMounted } from 'vue';
import Modal from './components/Modal.vue';
import CustomersTable from './components/CustomersTable.vue';

const showModal = ref(false);
const customers = ref([]);
const showCustomersTable = ref(false);



////show costomers 
async function fetchCustomers() {
  try {
    const response = await fetch('http://localhost:3000/api/customers');
    const data = await response.json();
    console.log("data", data);  
    customers.value = data;
  } catch (error) {
    console.error('Error fetching customers:', error);
  }
}

async function savedata() {
  console.log("saving data...");
 
  await fetchCustomers();  // if u dont want to show list after add user just remove this line 
  showModal.value = false; // close the modal
}

function toggleCustomersTable() {
  showCustomersTable.value = !showCustomersTable.value;
  if (showCustomersTable.value) {
    console.log("getting data ..")
    fetchCustomers();
  }
}

// fetch customers on component mount
onMounted(() => {
  fetchCustomers();
});
</script>

<template>
  <div class="container">
    <h1>Welcome To Passion Managers</h1>

    <div class="config-buttons">
      <button class="add-button" @click="showModal = true">
        Add Customers
      </button>

      <button class="show-button" @click="toggleCustomersTable">
        {{ showCustomersTable ? 'Hide' : 'Show' }} Customers
      </button>
    </div>

    <CustomersTable :show="showCustomersTable" :customers="customers" />

  
  </div>

  <Teleport to="body">
    <modal :show="showModal" @close="showModal = false" @save="savedata">
      <template #header>
        <h1>Add Customers form</h1>
      </template>
    </modal>
  </Teleport>
</template>

<style scoped>
.add-button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.show-button {
  background-color: #008CBA;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

.config-buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin-bottom: 20px;
}

</style>