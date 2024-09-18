<template>
  <div class="card">
    <img :src="imgSrc" alt="Blog Image" class="card-img" />
    <h3 class="card-title">{{ title }}</h3>

    <NuxtLink :to="{ name: 'blog-id', params: { id: id } }" class="card-button">
      Read articule
    </NuxtLink>
  </div>
</template>

<script setup>
const props = defineProps({
  imgSrc: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  id: {
    type: Number,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
});
</script>

<style scoped>
.card {
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  text-align: center;
}

.card-img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card-title {
  font-size: 1.5rem;
  color: #333;
  margin: 15px 0;
}

.card-button {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  margin-bottom: 15px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.card-button:hover {
  background-color: #0056b3;
}
</style>
