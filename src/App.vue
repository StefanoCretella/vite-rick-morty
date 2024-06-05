<template>
  <div id="app">
    <Header />
    <div class="search-container">
      <input v-model="searchName" placeholder="Search by name" />
      <select v-model="searchStatus">
        <option value="">Select Status</option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button @click="searchCharacters">Search</button>
      <button @click="resetSearch">Reset</button>
    </div>
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
      characters: [],
      searchName: '',
      searchStatus: ''
    };
  },
  async created() {
    this.fetchCharacters();
  },
  methods: {
    async fetchCharacters() {
      const response = await fetch('https://rickandmortyapi.com/api/character');
      const data = await response.json();
      this.characters = data.results;
    },
    async searchCharacters() {
      const nameQuery = this.searchName ? `&name=${this.searchName}` : '';
      const statusQuery = this.searchStatus ? `&status=${this.searchStatus}` : '';
      const response = await fetch(`https://rickandmortyapi.com/api/character?${nameQuery}${statusQuery}`);
      const data = await response.json();
      this.characters = data.results;
    },
    resetSearch() {
      this.searchName = '';
      this.searchStatus = '';
      this.fetchCharacters();
    }
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

.search-container {
  display: flex;
  gap: 1rem;
  margin: 1rem 0;
}
</style>
