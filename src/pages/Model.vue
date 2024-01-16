<template>
  <div class="background-section">
    <div class="content-overlay">
      <div class="col-md-5 col-xs-12">
        <h1 class="overlay-text">Find the perfect employee in our database of more than 25,000 new multilingual candidates each month.</h1>
      </div>
    </div>
  </div>
</template>

<style scoped>
.background-section {
  position: relative;
  width: 100%;
  height: 550px;
  background-image: url('src/statics/images/negocio.jpeg');
  background-size: cover;
  background-position: center;
}

.content-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(16, 98, 155, 0.84);
  display: flex;
  color: white;
}

.overlay-text {
  color: white;
  font-weight: bold;
  text-align: left;
  max-width: 80%; /* Ajusta según tus necesidades */
  margin-top: 20px;
}
</style>
