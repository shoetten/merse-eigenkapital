<script setup lang="ts">
import { computed } from '@vue/reactivity'
import { onMounted, ref } from 'vue'
import CountUp from 'vue-countup-v3'

const current = ref(0)
const total = ref(0)
const isLoading = ref(true)

onMounted(async () => {
  const response = await fetch('https://merse88b.de/wp-json/wp/v2/pages/103')
  const body = await response.json()
  current.value = body['acf']['eigenkapital_current']
  total.value = body['acf']['eigenkapital_total']
  isLoading.value = false
})

const relativeProgress = computed(() => (current.value !== 0 ? current.value / total.value * 100 : 0))

const formatter = new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'EUR', maximumFractionDigits: 0, minimumIntegerDigits: 6 })
</script>

<template>
  <div class="donation-meter">
    <div class="text">
      <strong>Wir brauchen</strong>
      <h3 class="goal">
        <count-up :end-val="total" :duration="1" :options="{ formattingFn: formatter.format}" />
      </h3>
    </div>
    <div class="thermometer">
      <span class="glass">
        <strong class="total" :style="{ bottom: `calc(${relativeProgress}% + var(--amount-inset))` }">
          <count-up :end-val="current" :duration="1" :options="{ formattingFn: formatter.format}" />
        </strong>
        <span class="amount" :style="{ height: relativeProgress + '%' }"></span>
      </span>
      <div class="bulb">
          <span class="bottom-circle"></span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.donation-meter {
  --glass-padding: min(0.3rem, 6px);
  --amount-inset: -10px;

  min-height: max(550px, 70vh);
  display: grid;
  grid-template-rows: auto 1fr;
  justify-items: center;
  gap: 1rem;

  padding: 3rem;
  backdrop-filter: blur(5px);
  border-radius: 1rem;

  .thermometer {
    display: flex;
    flex-direction: column;
    align-items: center;

    width: 60px;
  }

  .glass {
    background: #e5e5e5;
    border-radius: 100px 100px 0 0;
    display: block;
    height: 100%;
    padding: var(--glass-padding);
    position: relative;
    width: 50%;
  }
  .amount {
    background: var(--color-primary);
    border-radius: 100px;
    display: block;
    width: calc(100% - 2*var(--glass-padding));
    position: absolute;
    bottom: var(--amount-inset);
    z-index: 30;
    height: 0;

    transition: height 0.8s ease-out;
  }

  strong { display: block; text-align: center; }
  .goal {
    font-size: 2rem;
    margin: 0;
  }
  .total {
    font-size: 1rem;
    position: absolute;
    right: calc(100% + 2*var(--glass-padding));
    bottom: 0;
    transition: bottom 0.8s ease-out;
  }
}

.bulb {
  background: #e5e5e5;
  border-radius: 100%;
  display: block;
  padding: var(--glass-padding);
  position: relative;
  top: -20px;
  width: 100%;
  aspect-ratio: 1;

  .bottom-circle {
    background: var(--color-primary);
    border-radius: 100px;
    display: block;
    height: 100%;
    width: 100%;
  }
}
</style>
