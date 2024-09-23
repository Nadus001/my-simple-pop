<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <a href="">
      <img src="./assets/headerPig.png" class="logo vue" width="600" height="111" />
    </a>

    <p>Caution: This is not a bucket list. Completion of all items on this test will likely result in death.</p>
  </div>
  <HelloWorld />
</template>

<style scoped>
.logo {
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 4em #42b883aa);
}

p{
  color: #1a1a1a;
  font-weight: bold;
}

@media (max-width: 600px) {
  .logo {
    width: 300px;
    height: 50px;
    padding: 5px;
  }
}
</style>
