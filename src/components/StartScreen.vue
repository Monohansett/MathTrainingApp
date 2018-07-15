<template>
  <div class="container">
    <h3>Are You Ready?</h3>
    <button 
     class="ready-btn"
     @click="$emit('onStart')"
    > 
      Ready! 
    </button>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.container {
  text-align: center;
}

h3,
.btn {
  padding: 10px;
  margin: 25px 0;
  color: indigo;
  font-style: italic;
  font-family: "Bitter";
}

.ready-btn {
  background-color: transparent;
  border: solid 2px;
  border-color: indigo;
  transform: skewX(-20deg);
  color: indigo;
  padding: 5px;
  text-transform: uppercase;
  font-weight: bold;
}
.ready-btn:hover {
  background-color: indigo;
  color: white;
  cursor: pointer;
}
</style>

