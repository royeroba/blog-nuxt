<template>
  <div>
    <section class="hero">
      <div class="hero-content">
        <img src="/public/assets/img/hero.png" alt="hero" class="hero-image" />
        <div class="hero-overlay">
          <h1 class="hero-title">
            Sports and Video Games: Unlimited Passion in Two Worlds
          </h1>

          <NuxtLink :to="{ name: 'contact' }" class="hero-button">
            Contact us
          </NuxtLink>
        </div>
      </div>
    </section>

    <section class="description">
      <p>
        Welcome to “Sports and Video Games: Unlimited Passion in Two Worlds”!
        Dive into a universe where the adrenaline of sports meets the excitement
        of video games. On our blog, you’ll find the latest news on video games,
        keeping you updated with the newest releases and updates of your
        favorite games. Additionally, we bring you the most relevant sports news
        from around the world, from the most impressive goals to the most
        memorable plays.
      </p>
    </section>

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
  </div>
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
.hero {
  position: relative;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  overflow: hidden;
}

.hero-image {
  width: 100%;
  height: auto;
}

.hero-overlay {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: white;
}

.hero-title {
  font-size: 3rem;
  color: white;
  margin-bottom: 20px;
  text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.7);
}

.hero-button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
}

.hero-button:hover {
  background-color: #0056b3;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }

  .hero-button {
    padding: 8px 16px;
  }
}

.description {
  text-align: center;
  padding: 2rem;
  font-size: 1.25rem;
  color: #555;
}

.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  padding: 2rem;
}
</style>
