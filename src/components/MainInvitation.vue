<script setup>
  import IconHeart from "@/components/icons/IconHeart.vue";
  import ButtonChoice from "@/components/ButtonChoice.vue";
  import ImageTierra from "@/components/icons/ImageTierra.vue";

</script>

<template>
  <div class="container  text-center ">
    <div class="flex items-center justify-center w-full h-full">
      <div v-if="!decision" class="flex flex-col gap-y-5 z-2 font-family-1">
        <p class="pb-5 text-white text-2xl">Hi Midsy!</p>
        <div class="relative flex items-center justify-center">
          <IconHeart class="absolute" style="z-index:-1" :size="180" :color1="'fill:#fe9fb4;'" :color2="'fill:#fe9fb4;'"/>
          <p class="text-8xl cursive-text">14<sup>th</sup></p>
        </div>
        <p class="text-2xl pt-10 text-white">FEBUARY</p>
        <div class="text-white border-y-1 py-5 border-solid">Would you do me the honor of being my Valentine’s date?</div>
        <div class="block md:flex gap-x-5 justify-between pt-8 items-center">
          <ButtonChoice :update-decision="updateDecision"/>
        </div>
      </div>
      <div v-else-if="(payload && payload.decision === 'no') || decision === 'no'" class="flex flex-col gap-y-5 z-2 font-family-1">
        <div class="text-white text-lg">
          <p class="pb-5">I understand, thank you for confirming. . .</p>
        </div>
      </div>
      <div v-else-if="(payload && payload.decision === 'yes') || decision === 'yes' " class="flex flex-col gap-y-5 z-2 font-family-1">
        <div class="text-white text-lg">
          <p class="text-">YAY! I'll be Expecting</p>
          <p class="text-5xl">You!</p>
        </div>
        <div class="rounded overflow-hidden opacity-75 py-5 max-w-sm">
          <ImageTierra/>
        </div>
        <div class="text-white pt-10 text-lg">
          <p class="pb-5">Tierra Alta Palinpinon, <br>Valencia, Negros Oriental</p>
          <p>6:00 PM Onwards</p>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      decision: '',
      payload: null,
    }
  },
  mounted() {
    const savedPayload = localStorage.getItem('decisionPayload');
    if (savedPayload) {
      this.payload = JSON.parse(savedPayload);
      this.decision = this.payload.decision;
      console.log('Payload loaded from localStorage:', this.payload);
    } else {
      console.log('No payload found in localStorage.');
    }
  },
  methods: {
    updateDecision(value) {
      this.decision = value; // Update the decision when child emits
    },
  },
}
</script>

<style scoped>
  .container{
    height: 90vh;
    padding: 2rem;
    background:#890b30;
    border-radius: .5rem;
  }
  .cursive-text,sup {
    font-family: 'Dancing Script', cursive;
    color: #4a4a4a;
    font-weight: bold;
    background: linear-gradient(45deg, #890b30, #750527);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.3);
  }
  .font-family-1{
    font-family: 'PT Serif', serif;
  }
</style>
