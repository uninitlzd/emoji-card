<script setup>
import EmojiCard from './components/EmojiCard.vue'
</script>

<template>
  <main>
    <EmojiCard />
  </main>
</template>

<style>
@import './assets/base.css';

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

body {
  overflow: hidden;
}

.reset-button {
    margin: 0 auto;
}
</style>
