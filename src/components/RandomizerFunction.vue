<template>
  <div class="randomizer">
    <button @click="randomizeCard">Randomize</button>
  </div>
</template>

<script>
export default {
  methods: {
    randomizeCard() {
      this.$emit('randomize');
    }
  }
};
</script>

<style scoped>
.randomizer {
  display: flex;
  justify-content: flex-end;
  padding: 10px;
}

.randomizer button {
  background-color: #d4a017;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 18px;
  border-radius: 5px;
}
</style>
