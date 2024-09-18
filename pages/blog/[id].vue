<template>
  <div v-if="article" class="blog-container">
    <div class="blog-header">
      <img :src="article.img" alt="Article Image" class="blog-image" />
      <h1 class="blog-title">{{ article.title }}</h1>
    </div>
    <div class="blog-content">
      <p class="blog-description">{{ article.description }}</p>
    </div>
  </div>

  <div v-else>
    <h2>Article not found</h2>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const article = ref(null);
const articles = ref([]);

const loadArticle = (id) => {
  const selectedArticle = articles.value.find(
    (item) => item.id === parseInt(id)
  );
  if (selectedArticle) {
    article.value = selectedArticle;
  } else {
    console.error("Artículo no encontrado");
  }
};

onMounted(async () => {
  try {
    const response = await fetch("/assets/data/blog_articles.json");
    if (!response.ok) {
      throw new Error("Error loading the JSON: " + response.statusText);
    }
    const data = await response.json();
    articles.value = data.articles;

    if (route.params.id) {
      loadArticle(route.params.id);
    }
  } catch (error) {
    console.error(error.message);
  }
});
</script>

<style scoped>
.blog-container {
  margin: 6rem auto;
  max-width: 800px;
  padding: 1rem;
  background-color: #fff;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.blog-header {
  text-align: center;
  position: relative;
  overflow: hidden;
  border-radius: 10px;
}

.blog-image {
  width: 100%;
  height: auto;
  max-height: 400px;
  object-fit: cover;
  border-radius: 10px;
  transition: transform 0.3s ease;
}

.blog-title {
  font-size: 2rem;
  color: #333;
  margin-top: 1rem;
  text-transform: capitalize;
  font-weight: 700;
}

.blog-content {
  padding: 1.5rem 1rem;
  text-align: center;
}

.blog-description {
  font-size: 1.2rem;
  color: #555;
  line-height: 1.6;
  margin-top: 1rem;
  text-align: justify;
}

.blog-image:hover {
  transform: scale(1.05);
}

@media (max-width: 768px) {
  .blog-container {
    margin: 4rem;
    padding: 1rem;
  }

  .blog-title {
    font-size: 1.5rem;
  }

  .blog-description {
    font-size: 1rem;
  }

  .blog-image {
    max-height: 250px;
  }
}

@media (max-width: 480px) {
  .blog-title {
    font-size: 1.2rem;
  }

  .blog-description {
    font-size: 0.9rem;
  }
}
</style>
