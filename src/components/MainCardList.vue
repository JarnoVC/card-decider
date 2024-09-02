<template>
    <div class="card-display">
      <Card v-for="card in cards" :key="card.id" :card="card"  @click="flipCard(card.id)" />
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
  grid-template-columns: repeat(5, 1fr);
  gap: 100px; /* Reduced gap to avoid excessive spacing */
  padding: 50px;
  overflow: visible; /* Ensure the grid allows overflow */
  position: relative;
}



  /* Responsive adjustments */
  @media (max-width: 2000px) {
    .card-display {
      grid-template-columns: repeat(4, 1fr); /* 4 columns for medium screens */
      gap: 100px;
      padding: 15px;
    }
  }

  @media (max-width: 992px) {
    .card-display {
      grid-template-columns: repeat(3, 1fr); /* 3 columns for smaller screens */
      gap: 100px;
      padding: 10px;
    }
  }

  @media (max-width: 768px) {
    .card-display {
      grid-template-columns: repeat(2, 1fr); /* 2 columns for tablets */
      gap: 100px;
      padding: 5px;
    }
  }

  @media (max-width: 576px) {
    .card-display {
      grid-template-columns: 1fr; /* 1 column for mobile devices */
      gap: 100px;
      padding: 5px;
    }
  }
 
</style>
  