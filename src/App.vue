<template>
  <div id="app">
    <Header />
    <CharacterList :characters="characters" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import CharacterList from './components/CharacterList.vue';

export default {
  components: { Header, CharacterList },
  data() {
    return {
      characters: []
    };
  },
  async created() {
    const response = await fetch('https://rickandmortyapi.com/api/character');
    const data = await response.json();
    this.characters = data.results;
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

body {
  font-family: 'Montserrat', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
