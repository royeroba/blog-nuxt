<template>
  <div class="container">
    <div class="contact-text">
      <h2>Connect with Us!</h2>
      <p>Got questions or comments? We’re here to help!</p>
      <p>Fill out the form and we’ll get back to you soon.</p>
    </div>

    <div class="contact-form">
      <ContactForm />
    </div>
  </div>
</template>

<style scoped>
.container {
  margin-top: 10rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.contact-text {
  flex: 1;
}

.contact-form {
  flex: 1;
}

h2 {
  color: #333;
  font-size: 2rem;
}

@media (max-width: 768px) {
  .contact-form {
    max-width: 100%;
    flex: none;
  }

  .container {
    margin-top: 5rem;
    flex-direction: column;
    align-items: center;
  }
}
</style>
