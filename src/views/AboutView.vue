<template>
  <div class="about">
    <h1>Qui suis-je ?</h1>
    <div class="info">
      <h3>Nom : JACOB</h3>
      <h3>Prénom : Paul</h3>
      <h3>Promotion : LP MIAW 2024</h3>

    </div>
  </div>
</template>

<style scoped>
.about {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  color: #333;
  border-bottom: 2px solid #333;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

.info {
  background-color: #f2f2f2;
  padding: 20px;
  border-radius: 5px;
}

h3 {
  margin-bottom: 10px;
  color: #333;
}

@media (max-width: 600px) {
  .about {
    padding: 10px;
  }
}
</style>
