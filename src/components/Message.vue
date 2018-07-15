<template>
  <div class="alert" grid-list-xl text-xs-center>
      <h2>{{ text }}</h2>
      <button class="btn btn-primary" @click="$emit('onNext')"> 
        Continue 
      </button>
  </div>
</template>

<script>
export default {
  props: ["type", "text"]
};
</script>

<style scoped>
.alert {
  text-align: center;
}

h2 {
  margin: 20px 0;
}
</style>

