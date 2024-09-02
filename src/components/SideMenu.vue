<template>
  <div class="side-menu">
    <h2>Selected Card</h2>
    <div v-if="selectedCard" class="selected-card">
      <Card :card="selectedCard" :disableHover="true" />
      <div class="card-details">
        <h3>{{ selectedCard.name }}</h3>
        <p>Type: {{ selectedCard.type }}</p>
        <p>Effect: {{ selectedCard.effect }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './SingleCard.vue';

export default {
  components: { Card },
  props: {
    selectedCard: {
      type: Object,
      required: false,
    },
  },
};
</script>

<style scoped>
@font-face {
  font-family: 'FantasyFont';
  src: url('../assets/Fantasyfont.TTF') format('truetype');
  font-weight: normal;
  font-style: normal;
}

.side-menu {
  padding: 20px;
  background-color: #e3c99f;
  border-left: 2px solid #c19a6b;
  width: 350px; /* Increase width */
  box-sizing: border-box; /* Ensure padding and border are included in width */
}

.side-menu h2 {
  font-family: 'FantasyFont', sans-serif;
  font-size: 32px;
  color: #d4af37; /* Slightly darkened gold color */
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.8); /* Reduce the shadow blur to make the text sharper */
  padding-bottom: 10px;
  margin-top: -5px;
  background: rgba(0, 0, 0, 0.2); /* Add a semi-transparent background to enhance readability */
  text-align: center;
  border-radius: 5px; /* Add slight rounding for a softer look */
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2); /* Add a subtle box shadow to lift the text */
}

.side-menu h2::after {
  content: '';
  display: block;
  margin: 10px auto 0;
  width: 60%; /* Widen the decorative line slightly */
  height: 2px;
  background-color: #c19a6b;
}

.selected-card {
  display: flex;
  flex-direction: column; /* Stack the card and the details vertically */
  align-items: center; /* Center the content horizontally */
  margin-top: 50px; /* Add some margin between the title and the card */
}

.selected-card .card-details {
  text-align: center; /* Center the text below the card */
  margin-top: 20px; /* Add some space between the card and the text */
}

.selected-card h3 {
  font-size: 24px;
  color: #333;
}

.selected-card p {
  font-size: 18px;
  color: #666;
  margin: 5px 0; /* Add margin between the type and effect */
}
</style>
