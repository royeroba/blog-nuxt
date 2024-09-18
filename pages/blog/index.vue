<template>
  <section class="blog-grid">
    <Card
      v-for="article in articles"
      :key="article.id"
      :id="article.id"
      :="article"
      :imgSrc="article.img"
      :title="article.title"
    />
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";

const articles = ref([]);

onMounted(async () => {
  try {
    const response = await fetch("/assets/data/blog_articles.json");
    if (!response.ok) {
      throw new Error("Error loading the JSON: " + response.statusText);
    }
    const data = await response.json();
    articles.value = data.articles;
  } catch (error) {
    console.error(error.message);
  }
});
</script>
<style scoped>
.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  padding: 2rem;
  margin-top: 6rem;
}
</style>
