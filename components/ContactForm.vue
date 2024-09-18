<template>
  <div class="card">
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          type="text"
          id="name"
          v-model="name"
          placeholder="Type your name"
        />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>
      </div>

      <div class="form-group">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          v-model="email"
          placeholder="Type your email"
        />
        <span v-if="errors.email" class="error">{{ errors.email }}</span>
      </div>

      <div class="form-group">
        <label for="phone">Phone</label>
        <input
          type="tel"
          id="phone"
          v-model="phone"
          placeholder="Type your phone"
        />
        <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
      </div>

      <div class="form-group">
        <label for="message">Tell us</label>
        <textarea
          id="message"
          v-model="message"
          placeholder="Type your comments"
        ></textarea>
        <span v-if="errors.message" class="error">{{ errors.message }}</span>
      </div>

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const form = reactive({
  name: "",
  email: "",
  phone: "",
  message: "",
});

const errors = reactive({
  name: null,
  email: null,
  phone: null,
  message: null,
});

const validateForm = () => {
  let valid = true;

  if (!form.name) {
    errors.name = "Name is required";
    valid = false;
  } else {
    errors.name = null;
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!form.email) {
    errors.email = "Email is required";
    valid = false;
  } else if (!emailRegex.test(form.email)) {
    errors.email = "The email is not valid";
    valid = false;
  } else {
    errors.email = null;
  }

  const phoneRegex = /^[0-9]{10}$/;
  if (!form.phone) {
    errors.phone = "Phone is required";
    valid = false;
  } else if (!phoneRegex.test(form.phone)) {
    errors.phone = "The phone number must have 10 digits";
    valid = false;
  } else {
    errors.phone = null;
  }

  if (!form.message) {
    errors.message = "The message is required";
    valid = false;
  } else {
    errors.message = null;
  }

  return valid;
};

const submitForm = () => {
  if (validateForm()) {
    alert("Form sent successfully");
  }
};
</script>

<style scoped>
.card {
  max-width: 500px;
  width: 100%;
  padding: 2rem;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 2rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

input,
textarea {
  width: 100%;
  padding: 0.5rem;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 1rem;
}

textarea {
  resize: vertical;
  min-height: 100px;
}

button {
  padding: 0.75rem 1.5rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  width: 100%;
}

button:hover {
  background-color: #0056b3;
}

.error {
  color: red;
  font-size: 0.875rem;
  margin-top: 0.5rem;
}
</style>
