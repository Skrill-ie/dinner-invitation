<script setup>

</script>

<template>
  <button class="button-82-pushable w-full" role="button" @click="setDecision('yes')">
    <span class="button-82-shadow"></span>
    <span class="button-82-edge"></span>
    <span class="button-82-front text">
      <span v-if="clickCount <= 2">YES</span>
      <span v-else-if="clickCount <= 4">Button "No" not working?? <br>Try Pressing Yes. . </span>
      <span v-else-if="clickCount <=6">You're Being Hard to get :/</span>
      <span v-else-if="clickCount <= 8">Really? Still a No?</span>
      <span v-else-if="clickCount >= 9">Last Chance . . .</span>
    </span>
  </button>
  <div class="pt-5 md:pt-0" v-if="currentOpacity > 0" :style="{ opacity: currentOpacity }">
    <button class="button-82-pushable w-full" role="button" @click="handleClick('no')">
      <span class="button-82-shadow"></span>
      <span class="button-82-edge"></span>
      <span class="button-82-front text">
        NO
      </span>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      clickCount: 0, // Tracks the number of clicks
    };
  },
  props: {
    updateDecision: {
      type: Function,
      required: true,
    },
  },
  computed: {
    currentOpacity() {
      return Math.max(1 - this.clickCount * 0.1, 0);
    },
  },
  methods: {
    async setDecision(value) {
      const payload = {
        userId: 'midsy', // Replace with actual user ID
        decision: 'yes',
      };
      this.updateDecision(payload.decision);
      localStorage.setItem('decisionPayload', JSON.stringify(payload));

      const apiResponse = await this.handleApi(payload);

      if (apiResponse) {
        console.log('Decision saved successfully:', apiResponse);
      }
    },
    async handleClick() {
      if (this.currentOpacity > 0) {
        this.clickCount++; // Increment click count only if opacity is above 0
        console.log(this.clickCount)
      }
      if (this.clickCount === 10) {
        const payload = {
          userId: 'midsy', // Replace with actual user ID
          decision: 'no',
        };
        this.updateDecision(payload.decision);
        localStorage.setItem('decisionPayload', JSON.stringify(payload));

        const apiResponse = await this.handleApi(payload);

        if (apiResponse) {
          console.log('Decision saved successfully:', apiResponse);
        }
      }
    },
    async handleApi(payload) {
    try {
      const response = await fetch('https://script.google.com/macros/s/AKfycbzLSYMel4xGFG_T0_LpI4VW_G-8TZK2h-j0uS0LEuBYpdSw8F98lqewDR1wWuLUdtct/exec', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(payload), mode: "no-cors"
      });

      if (!response.ok) {
        throw new Error('Failed to fetch API');
      }

      const data = await response.json();
      console.log('API response:', data);
      return data; // Return data for further use
    } catch (error) {
      console.error('Error in handleApi:', error);
    }
  },
  },

};
</script>

<style scoped>
.button-82-pushable {
  position: relative;
  border: none;
  background: transparent;
  padding: 0;
  cursor: pointer;
  outline-offset: 4px;
  transition: filter 250ms, opacity 0.3s ease;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}
.button-82-pushable-no{
  transition: opacity 0.3s ease;
}

.button-82-shadow {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 12px;
  background: hsl(0deg 0% 0% / 0.25);
  will-change: transform;
  transform: translateY(2px);
  transition:
      transform
      600ms
      cubic-bezier(.3, .7, .4, 1);
}

.button-82-edge {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 12px;
  background: linear-gradient(
      to left,
      hsl(340deg 100% 16%) 0%,
      hsl(340deg 100% 32%) 8%,
      hsl(340deg 100% 32%) 92%,
      hsl(340deg 100% 16%) 100%
  );
}

.button-82-front {
  display: block;
  position: relative;
  padding: 12px 27px;
  border-radius: 12px;
  font-size: 1.1rem;
  color: #890b30;
  background: #fe9fb4;
  will-change: transform;
  transform: translateY(-4px);
  transition:
      transform
      600ms
      cubic-bezier(.3, .7, .4, 1);
}

@media (min-width: 768px) {
  .button-82-front {
    font-size: 1.25rem;
    padding: 12px 42px;
  }
}

.button-82-pushable:hover {
  filter: brightness(110%);
  -webkit-filter: brightness(110%);
}

.button-82-pushable:hover .button-82-front {
  transform: translateY(-6px);
  transition:
      transform
      250ms
      cubic-bezier(.3, .7, .4, 1.5);
}

.button-82-pushable:active .button-82-front {
  transform: translateY(-2px);
  transition: transform 34ms;
}

.button-82-pushable:hover .button-82-shadow {
  transform: translateY(4px);
  transition:
      transform
      250ms
      cubic-bezier(.3, .7, .4, 1.5);
}

.button-82-pushable:active .button-82-shadow {
  transform: translateY(1px);
  transition: transform 34ms;
}

.button-82-pushable:focus:not(:focus-visible) {
  outline: none;
}
</style>