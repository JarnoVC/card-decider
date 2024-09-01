<template>
    <div class="card-display">
      <Card v-for="card in cards" :key="card.id" :card="card" @click="flipCard(card.id)" />
    </div>
  </template>
  
  <script>
  import Card from './SingleCard.vue';
  
  export default {
    components: { Card },
    props: ['cards'],
    methods: {
      flipCard(id) {
        this.$emit('flip-card', id);
      }
    }
  };
  </script>
  
  <style scoped>
  .card-display {
    display: grid;
    grid-template-columns: repeat(5, 1fr); /* Adjust columns as needed */
    gap: 80px; /* This adds space between both rows and columns */
    padding: 50px;
}
  </style>
  