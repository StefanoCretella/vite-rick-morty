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
    <Pagination 
      v-if="totalPages > 1" 
      :currentPage="currentPage" 
      :totalPages="totalPages" 
      @updatePage="updatePage"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import CharacterList from './components/CharacterList.vue';
import Pagination from './components/Pagination.vue';

export default {
  components: { Header, CharacterList, Pagination },
  data() {
    return {
      characters: [],
      searchName: '',
      searchStatus: '',
      currentPage: 1,
      totalPages: 1  // Assicurati che totalPages sia definito qui
    };
  },
  async created() {
    this.fetchCharacters();
  },
  methods: {
    async fetchCharacters(page = 1) {
      const nameQuery = this.searchName ? `&name=${this.searchName}` : '';
      const statusQuery = this.searchStatus ? `&status=${this.searchStatus}` : '';
      const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page}${nameQuery}${statusQuery}`);
      const data = await response.json();
      this.characters = data.results;
      this.totalPages = data.info.pages;
    },
    searchCharacters() {
      this.currentPage = 1;
      this.fetchCharacters();
    },
    resetSearch() {
      this.searchName = '';
      this.searchStatus = '';
      this.currentPage = 1;
      this.fetchCharacters();
    },
    updatePage(page) {
      this.currentPage = page;
      this.fetchCharacters(page);
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
