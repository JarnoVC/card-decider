<template>
    <div class="side-menu">
      <h2>Selected Card</h2>
      <div v-if="selectedCard" class="selected-card">
        <Card :card="selectedCard" />
      </div>
    </div>
  </template>
  
  <script>
  import Card from './SingleCard.vue';
  
  export default {
    components: { Card },
    props: ['selectedCard']
  };
  </script>
  
  <style scoped>
  .side-menu {
    padding: 20px;
    background-color: #e3c99f;
    border-left: 2px solid #c19a6b;
    width: 350px; /* Increase width */
    box-sizing: border-box; /* Ensure padding and border are included in width */
  }
  
  .selected-card {
    display: block; /* Display as block to take full width */
    margin-top: 50px; /* Add some margin between the title and the card */
  }
  </style>
  