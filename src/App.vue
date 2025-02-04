<script setup>
  import Floating from '@/components/object/FloatingHeart.vue'
  import MainInvitation from "@/components/MainInvitation.vue";
  // import IconHeart from "@/components/icons/IconHeart.vue";
  import ImageRose from "@/components/icons/ImageRose.vue";
</script>

<template>
  <Floating/>
  <main class="flex justify-center">
    <div class="wrapper ">
      <div class="relative overflow-hidden">
        <div style="opacity: 60%; filter: drop-shadow(0 0 0.75rem #4d0017) blur(3px);">
          <image-rose style="width: 19rem; top:-7rem; left:-30%;"/>
          <image-rose style="width: 15rem; top:-7rem; left: 22%; z-index: 1"/>
          <image-rose style="width: 19rem; top:-7rem; left: 60%;"/>
        </div>
        <MainInvitation/>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    //place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
