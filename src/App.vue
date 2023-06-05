<template>
  <main>
    <div>
      <h4>The courrent count is ...</h4>
      <h1>{{ count }}</h1>
      <div class="button-div">
        <button @click="$event => count--">-</button>
        <button @click="$event => count++">+</button>
      </div>
    </div>
  </main>
</template>

<script setup>
  import { ref } from 'vue';
  const count = ref(0);

</script>

<style scoped>
  

  main {
    background-color: aliceblue;
    height: 100vh;
    width: 100vw;

    display: flex;
    align-items: center;
    justify-content: center;
  }

  div {
    text-align: center;
  }

  h4 {
    font-size: 2rem;
  }
  .button-div {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
  }

  .button-div button {
    font-size: 2rem;
    height: 40px;
    width: 40px;

    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
