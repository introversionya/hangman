<script setup lang="ts">
import GameHeader from './components/GameHeader.vue'
import GameFigure from './components/GameFigure.vue'
import GameWrongLetters from './components/GameWrongLetters.vue'
import GameWord from './components/GameWord.vue'
import GamePopup from './components/GamePopup.vue'
import GameNotification from './components/GameNotification.vue'
import { ref, computed } from 'vue'

const word = ref('василий')
const letters = ref<string[]>([])
const correctLetters = computed(() => letters.value.filter((x) => word.value.includes(x)))
const wrongLetters = computed(() => letters.value.filter((x) => !word.value.includes(x)))

window.addEventListener('keydown', ({ key }) => {
  if (/[а-яА-ЯёЁ]/.test(key)) {
    letters.value.push(key.toLocaleLowerCase())
  }
})
</script>

<template>
  <GameHeader />

  <div class="game-container">
    <GameFigure />
    <GameWrongLetters :wrongLetters="wrongLetters" />
    <GameWord :word="word" :correctLetters="correctLetters" />
  </div>

  <GamePopup v-if="false" />
  <GameNotification />
</template>
