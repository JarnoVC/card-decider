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
        { id: 17, name: 'Northern winds', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/Northern winds_cutout.png'), flipped: false },
        { id: 18, name: 'The chronomancer', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The chronomancer_cutout.png'), flipped: false },
        { id: 19, name: 'The devil', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The devil_cutout.png'), flipped: false },
        { id: 20, name: 'The divergent', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The divergent_cutout.png'), flipped: false },
        { id: 21, name: 'The empyrean', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The empyrean_cutout.png'), flipped: false },
        { id: 22, name: 'The forest nymph', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The forest nymph_cutout.png'), flipped: false },
        { id: 23, name: 'The fountain', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The fountain_cutout.png'), flipped: false },
        { id: 24, name: 'The gavel', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The gavel_cutout.png'), flipped: false },
        { id: 25, name: 'The honorbound', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The honorbound_cutout.png'), flipped: false },
        { id: 26, name: 'The still', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The still_cutout.png'), flipped: false },
        { id: 27, name: 'The lovers', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The lovers_cutout.png'), flipped: false },
        { id: 28, name: 'The loving mother', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The loving mother_cutout.png'), flipped: false },
        { id: 29, name: 'The lurking shadow', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The lurking shadow_cutout.png'), flipped: false },
        { id: 30, name: 'The mirror', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The mirror_cutout.png'), flipped: false },
        { id: 31, name: 'The reaper', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The reaper_cutout.png'), flipped: false },
        { id: 32, name: 'The shadow', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The shadow_cutout.png'), flipped: false },
        { id: 33, name: 'The siren', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The siren_cutout.png'), flipped: false },
        { id: 34, name: 'The imp', effect: 'Buff: +10 Strength', imageUrl: require('@/assets/The imp_cutout.png'), flipped: false },
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
  min-height: 100vh;
  box-sizing: border-box;
  overflow: visible; /* Allow overflow in case of enlarged elements */
  position: relative;
}

main {
  display: flex;
  flex: 1;
  overflow: visible; /* Ensure the content in main can overflow without clipping */
  position: relative;
}


.card-display {
  flex: 3;
  position: relative; /* Ensure that cards within the grid can overflow */
  z-index: 1; /* Default z-index */
}

.random-result {
  flex: 1;
  padding: 20px;
  background-color: #e3c99f;
  border-left: 2px solid #c19a6b;
}
</style>
