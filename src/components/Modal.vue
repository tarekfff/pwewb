<script setup>
import { ref } from 'vue';

const props = defineProps({
    show: Boolean
});

const emit = defineEmits(['close', 'save']);

const name = ref('');
const email = ref('');
const phone = ref('');
const address = ref('');
const city = ref('');
const date = ref('');
const error = ref('');
const isLoading = ref(false);

const submitForm = async () => {
  error.value = '';
  
  // Basic validation
  if (!name.value || !email.value) {
    error.value = 'Name and email are required';
    return;
  }

  isLoading.value = true;
  
  try {
    const response = await fetch('http://localhost:3000/api/submit-form', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        name: name.value,
        email: email.value,
        phone: phone.value,
        address: address.value,
        city: city.value,
        date: date.value
      })
    });

    const data = await response.json();
    
    if (!response.ok) {
      throw new Error(data.error || 'Failed to submit form');
    }

    // Reset form on success
    name.value = '';
    email.value = '';
    phone.value = '';
    address.value = '';
    city.value = '';
    date.value = '';
    
    emit('save');
  } catch (err) {
    error.value = err.message;
    console.error('Submission error:', err);
  } finally {
    isLoading.value = false;
  }
};
</script>

<template>
    <Transition name="modal">
        <div v-if="show" class="modal-mask">
            <div class="modal-container">
                <div class="modal-header">
                    <slot name="header"></slot>
                </div>

                <div class="modal-body">
                    <div v-if="error" class="error-message">{{ error }}</div>
                    
                    <slot name="info">
                        <div class="form-group">
                            <label for="name">Name *</label>
                            <input type="text" id="name" v-model="name" placeholder="Name" required />
                        </div>

                        <div class="form-group">
                            <label for="email">Email *</label>
                            <input type="email" id="email" v-model="email" placeholder="Email" required />
                        </div>

                        <div class="form-group">
                            <label for="phone">Phone</label>
                            <input type="text" id="phone" v-model="phone" placeholder="Phone" />
                        </div>

                        <div class="form-group">
                            <label for="address">Address</label>
                            <input type="text" id="address" v-model="address" placeholder="Address" />
                        </div>

                        <div class="form-group">
                            <label for="city">City</label>
                            <input type="text" id="city" v-model="city" placeholder="City" />
                        </div>

                        <div class="form-group">
                            <label for="date">Date</label>
                            <input type="date" id="date" v-model="date" />
                        </div>
                    </slot>
                </div>

                <div class="modal-footer">
                    <button class="close-button" @click="$emit('close')" :disabled="isLoading">Close</button>
                    <button class="done-button" @click="submitForm" :disabled="isLoading">
                        <span v-if="isLoading">Saving...</span>
                        <span v-else>Done</span>
                    </button>
                </div>
            </div>
        </div>
    </Transition>
</template>

<style scoped>
.modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    transition: opacity 0.3s ease;
}

.modal-container {
    width: 450px;
    margin: auto;
    padding: 2rem;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
}

.modal-header {
    margin-bottom: 1.5rem;
}

.modal-header h1 {
    margin-top: 0;
    color: #42b983;
}

.modal-body {
    margin: 1.5rem 0;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.error-message {
    color: #ff4444;
    padding: 0.5rem;
    background-color: #ffeeee;
    border-radius: 4px;
    margin-bottom: 1rem;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.form-group label {
    font-weight: 500;
    color: #333;
}

.form-group input {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
}

.form-group input:focus {
    outline: none;
    border-color: #42b983;
    box-shadow: 0 0 0 2px rgba(66, 185, 131, 0.2);
}

.modal-footer {
    display: flex;
    justify-content: flex-end;
    margin-top: 1.5rem;
    gap: 5px;
}

.close-button {
    padding: 0.5rem 1rem;
    background-color: #f0f0f0;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.done-button {
    padding: 0.5rem 1rem;
    background-color: aqua;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.close-button:hover {
    background-color: #e0e0e0;
}

.close-button:disabled,
.done-button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

/* Transition effects */
.modal-enter-from {
    opacity: 0;
}

.modal-leave-to {
    opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
    transform: scale(1.1);
}
</style>