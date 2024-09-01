<template>
  <div class="app-container">
    <Randomizer @randomize="randomizeCard" />

    <main>
      <MainCardList :cards="cards" @flip-card="flipCard" />
      <SideMenu :selectedCard="selectedCard" />
    </main>
  </div>
</template>

<script>
import MainCardList from './components/MainCardList.vue';
import SideMenu from './components/SideMenu.vue';
import Randomizer from './components/RandomizerFunction.vue';

export default {
  components: { MainCardList, SideMenu, Randomizer },
  data() {
    return {
      cards: [
        { id: 1, name: 'Disappearing act', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/Disappearing act_cutout.png'), flipped: false },
        { id: 2, name: 'Spiral of time', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/Spiral of time_cutout.png'), flipped: false },
        { id: 3, name: 'Starless night', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/Starless night_cutout.png'), flipped: false },
        { id: 4, name: 'The betrayer', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The betrayer_cutout.png'), flipped: false },
        { id: 5, name: 'The butterfly', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The butterfly_cutout.png'), flipped: false },
        { id: 6, name: 'The collapse', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The collapse_cutout.png'), flipped: false },
        { id: 7, name: 'The echo', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The echo_cutout.png'), flipped: false },
        { id: 8, name: 'The fates', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The fates_cutout.png'), flipped: false },
        { id: 9, name: 'The hanged man', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The hanged man_cutout.png'), flipped: false },
        { id: 10, name: 'The incubus', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The incubus_cutout.png'), flipped: false },
        { id: 11, name: 'The leviathan', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The Leviathan2_cutout.png'), flipped: false },
        { id: 12, name: 'The shapeshifter', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The shapeshifter_cutout.png'), flipped: false },
        { id: 13, name: 'The thief', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The thief_cutout.png'), flipped: false },
        { id: 14, name: 'The thorned rose', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The thorned rose_cutout.png'), flipped: false },
        { id: 15, name: 'The twin', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The twin_cutout.png'), flipped: false },
        { id: 16, name: 'The valkyrie', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The valkyrie_cutout.png'), flipped: false },
        // Add the rest of your 40 cards here
      ],
      selectedCard: null
    };
  },
  methods: {
    randomizeCard() {
      const randomIndex = Math.floor(Math.random() * this.cards.length);
      this.selectedCard = this.cards[randomIndex];
    },
    flipCard(id) {
      this.cards = this.cards.map(card =>
        card.id === id ? { ...card, flipped: !card.flipped } : card
      );
    }
  }
};
</script>

<style scoped>
.app-container {
  border: 10px solid #c19a6b;
  background-color: #f5f5dc;
  padding: 20px;
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* Ensure the container takes at least full viewport height */
  box-sizing: border-box;
  overflow: hidden; /* Hide any overflow from within the container */
}

main {
  display: flex;
  flex: 1;
  overflow-y: auto; /* Allows scrolling if the content overflows vertically */
  overflow-x: hidden; /* Prevents horizontal overflow */
}

.card-display {
  flex: 3;
}

.random-result {
  flex: 1;
  padding: 20px;
  background-color: #e3c99f;
  border-left: 2px solid #c19a6b;
}
</style>
