<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <main>
    <header>
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    </header>

    <RouterView />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
}

.logo {
  display: block;
  margin: 0 auto 1rem;
}

h1 {
  color: #42b883;
  font-size: 2rem;
  margin-bottom: 2rem;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
}
</style>
