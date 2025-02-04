<script setup>
  import HeartIcon from '../icons/IconHeart.vue'
</script>

<template>
  <div class="background-container">
    <div class="floating-icon" v-for="n in 20" :key="n" :style="randomPosition()">
      <HeartIcon :color1="'fill:#890b30;'" :color2="'fill:#890b30;'" :size="randomSize()"/>
    </div>
  </div>
</template>

<style scoped>

</style>

<script>
export default {
  methods: {
    randomPosition() {
      // Generate random horizontal position and delay for each icon
      const left = Math.random() * 100; // Random percentage for horizontal position
      const delay = Math.random() * 3; // Random delay between 0-5 seconds
      return {
        left: `${left}%`,
        animationDelay: `${delay}s`,
      };
    },
    randomSize(){
      return Math.random() * 80 + 20;
    }
  },
};
</script>