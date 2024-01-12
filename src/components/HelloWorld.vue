<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>Your Voice Shapes the Future!</h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: 1px;

  margin-top: 15%;
}

h3 {
  font-size: 1.2rem;
  color: rgba(250, 249, 247, 0.658);
}

.greetings h1,
.greetings h3 {
  text-align: left;
  display: flex;
  place-items: flex-start;
  flex-wrap: wrap;
  margin-right: auto;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
