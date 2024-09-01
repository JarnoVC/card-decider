<template>
  <div class="card" @click="flipCard">
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
  props: ['card'],
  methods: {
    flipCard() {
      this.$emit('click');
    }
  }
};
</script>

<style scoped>
.card {
  width: 250px; /* Adjust to fit inside the grid */
  height: 400px; /* Ensure the card scales correctly */
  perspective: 1000px;
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
