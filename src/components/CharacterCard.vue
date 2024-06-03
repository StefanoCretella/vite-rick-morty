<template>
    <div class="character-card">
        <img :src="character.image" :alt="character.name">
        <h2>{{ character.name }}</h2>
        <p>Status: {{ character.status }}</p>
        <p>Spacies: {{ character.species }}</p>
    </div>
</template>

<script>
export default {
    props: {
        character: Object
    }
}
</script>

<style scoped>
.character-card {
    border: 1px solid #ddd;
    border-radius: 0.5rem;
    overflow: hidden;
    text-align: center;
    width: 200px;
}

.character-card img {
    width: 100%;
    height: auto;
}

.character-card h2 {
    font-size: 1.2rem;
    margin: 0.5rem 0;
}
</style>