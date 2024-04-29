<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { onMounted, ref } from 'vue'

const current = ref(0)
const total = ref(0)

onMounted(async () => {
  const response = await fetch('https://merse88b.de/wp-json/wp/v2/pages/103')
  const body = await response.json()
  current.value = body['acf']['eigenkapital_current']
  total.value = body['acf']['eigenkapital_total']
})

const relativeProgress = computed(() => (current.value / total.value * 100))

const formatter = new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'EUR', maximumFractionDigits: 0 })
</script>

<template>
  <div class="donation-meter">
    <strong>Wir brauchen</strong>
    <strong class="goal">{{ formatter.format(total) }}</strong>
    <span class="glass">
        <strong class="total" :style="`bottom: ${relativeProgress}%`">{{ formatter.format(current) }}</strong>
        <span class="amount" :style="`height: ${relativeProgress}%`"></span>
    </span>
    <div class="bulb">
        <span class="bottom-circle"></span>
        <span class="filler">
            <span></span>
        </span>
    </div>
  </div>
</template>

<style scoped>
.donation-meter {
  .glass {
    background: #e5e5e5;
    border-radius: 100px 100px 0 0;
    display: block;
    height: 300px;
    margin: 0 35px 10px;
    padding: 5px;
    position: relative;
    width: 20px;
  }
  .amount {
    background: var(--color-primary);
    border-radius: 100px;
    display: block;
    width: 20px;
    position: absolute;
     bottom: 5px;
  }
  strong { display: block; text-align: center; }
  .goal {
    font-size: 30px;
  }
  .total {
    font-size: 16px;
    position: absolute;
    right: 35px;
  }
}

.bulb {
  background: #e5e5e5;
  border-radius: 100px;
  display: block;
  height: 50px;
  margin: 0 35px 10px;
  padding: 5px;
  position: relative;
    top: -20px;
    right: 15px;
  width: 50px;
  .bottom-circle {
    background: var(--color-primary);
    border-radius: 100px;
    display: block;
    height: 50px;
    width: 50px;
  }
  .filler {
    background: var(--color-primary);
    border-radius: 100px 100px 0 0;
    display: block;
    height: 30px;
    width: 20px;
    position: relative;
      top: -65px;
      right: -15px;
    z-index: 30;
  }
}
</style>
