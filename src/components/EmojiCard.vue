<script setup>
import { computed, ref } from 'vue'

const emojis = [
  "Avocado.png",
  "Baby Chick.png",
  "Bear.png",
  "Bird.png",
  "Bug.png",
  "Dog Face.png",
  "Dolphin.png",
  "Fish.png",
  "Fox.png",
  "Gorilla.png",
  "Grapes.png",
  "Hamburger.png",
  "Hear No Evil Monkey.png",
  "Kiwi Fruit.png",
  "Lemon.png",
  "Pear.png",
  "Pineapple.png",
  "Red Apple.png",
  "Strawberry.png",
  "Tangerine.png",
];

const multiplyArray = (arr, length) => 
  Array.from({ length }, () => arr).flat()

const multipliedEmojiEntry = multiplyArray(emojis, 4)

function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
}

shuffleArray(multipliedEmojiEntry)

console.log(multipliedEmojiEntry)

const counter = ref(0)
const maxCounter = ref(multipliedEmojiEntry.length)

const incrementCounter = () => {
  counter.value++
}

const displayedEmoji = computed(() => {
  return `/emojis/${multipliedEmojiEntry[counter.value]}`
})


</script>

<template>
  <div class="card">
    <div class="emoji">
      <img @click="incrementCounter" :src="displayedEmoji" alt="" srcset="" />
    </div>
  </div>
</template>

<style>
.card {
  margin: 2rem auto;
  background: white;
  border-radius: 20px;
  height: calc(80vh - 4rem);
  width: calc(100vw - 4rem);
  display: flex;
  flex-direction: column;
  justify-content: center;
  box-shadow: 1px 1px;
  border: 1px solid rgb(226, 226, 226);
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
}

.card-1 {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}

.emoji {
  color: black;
  margin: 0 auto;
}

.emoji img {
  width: 72px;
  height: 72px;
}

</style>
