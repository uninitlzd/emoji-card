<script setup>
import { computed, onMounted, reactive, ref } from "vue";

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

const MULTIPLE_BY_4 = 4;

const multiplyArray = (arr, length) => Array.from({ length }, () => arr).flat();

function shuffleArray(array) {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
}

let emojiEntry = [];
const counter = ref(0);
const maxCounter = ref(emojis.length * MULTIPLE_BY_4);
const storedEntries = localStorage.getItem("entries");

const initCardStack = () => {
  const multipliedEmojiEntry = multiplyArray(emojis, MULTIPLE_BY_4);
  shuffleArray(multipliedEmojiEntry);

  localStorage.setItem("entries", JSON.stringify(multipliedEmojiEntry));
  localStorage.setItem("counter", 0);
  emojiEntry = multipliedEmojiEntry;
  counter.value = 0;
};

if (storedEntries === null) {
  initCardStack();
} else {
  emojiEntry = JSON.parse(storedEntries);
  counter.value = localStorage.getItem("counter");
}

var clickTimer;
const clickCounter = ref(0);
console.log(clickCounter.value);

const incrementCounter = () => {
  clickCounter.value++;
  if (clickCounter.value == 1) {
    clickTimer = setTimeout(function () {
      console.log(clickCounter.value);
      // DO NOTHING BUT RESET IN CASE THERES JUST ONE CLICK
      if (counter.value == maxCounter.value) {
        counter.value = 0;
      } else {
        counter.value++;
      }
      
      clickCounter.value = 0;
      console.log(clickCounter.value);
    }, 350); // increase delay as you like
  } else if (clickCounter.value === 3) {
    console.log("entry reset!");
    initCardStack();
    alert("Card stack reset");
  }

  localStorage.setItem("counter", counter.value);
};

const displayedEmoji = computed(() => {
  // console.log(emojiEntry)
  return `/emojis/${emojiEntry[counter.value]}`;
});
</script>

<template>
  <div class="card">
    <div class="emoji">
      <img
        @click="incrementCounter($event)"
        :src="displayedEmoji"
        alt=""
        srcset=""
      />
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
