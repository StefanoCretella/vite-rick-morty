<template>
    <div class="character-list">
      <CharacterCard v-for="character in characters" :key="character.id" :character="character" />
    </div>
  </template>
  
  <script>
  import CharacterCard from './CharacterCard.vue';
  
  export default {
    components: { CharacterCard },
    props: {
      characters: Array
    }
  }
  </script>
  
  <style scoped>
  .character-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: center;
    padding: 1rem;
  }
  </style>
  