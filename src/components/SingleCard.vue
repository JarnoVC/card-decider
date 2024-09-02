<template>
  <div class="card" :class="{ 'no-hover': disableHover }" @click="flipCard">
    <div class="card-inner" :class="{ flipped: card.flipped }">
      <div class="card-front">
        <img :src="card.imageUrl" alt="Card Image" class="card-image" />
      </div>
      <div class="card-back">
        {{ card.effect }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    card: Object,
    disableHover: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    flipCard() {
      if (!this.disableHover) {
        this.$emit('click');
      }
    }
  }
};
</script>

<style scoped>
.card {
  width: 250px;
  height: 400px;
  perspective: 1000px;
  transition: transform 0.3s ease;
  position: relative; /* Ensure the card can be layered above others */
}

.card:hover {
  transform: scale(1.2);
  z-index: 10; /* Bring the card to the front */
  overflow: visible; /* Ensure enlarged card is not clipped */
}

/* Disable hover effect when disableHover prop is true */
.no-hover:hover {
  transform: none;
  z-index: auto;
}

.card-inner {
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.card-inner.flipped {
  transform: rotateY(180deg);
}

.card-front, .card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18px;
}

.card-front {
  background-color: #fff;
}

.card-back {
  transform: rotateY(180deg);
  background-color: #f1c40f;
  color: black;
}

.card-image {
  width: 100%;
  height: auto;
  object-fit: contain; /* Ensures the image scales properly */
}
</style>
