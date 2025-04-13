<template>
  <div class="min-h-screen bg-yellow-50 flex flex-col items-center p-6">
    <h1 class="text-3xl font-bold mb-4">Eierlikoer With Me</h1>

    <div class="bg-white rounded-2xl shadow-xl p-6 w-full max-w-md flex flex-col items-center">
      <p class="text-xl font-medium mb-2">Ich trinke gerade:</p>
      <select v-model="selectedVariant" class="p-2 rounded border mb-4 w-full">
        <option disabled value="">Bitte waehlen...</option>
        <option>Eierlikoer pur</option>
        <option>Eierlikoer mit Wodka</option>
        <option>Eierlikoer mit Rum</option>
        <option>Eierlikoer auf Eis</option>
        <option>Eierlikoer im Kaffee</option>
      </select>

      <button @click="checkIn" class="bg-yellow-500 hover:bg-yellow-600 text-white font-bold py-2 px-6 rounded-full">
        Check-in
      </button>
    </div>

    <div v-if="checkIns.length" class="mt-8 w-full max-w-md">
      <h2 class="text-xl font-semibold mb-2">Letzte Check-ins</h2>
      <ul class="bg-white rounded shadow divide-y divide-gray-200">
        <li v-for="(entry, index) in checkIns" :key="index" class="p-4">
          <strong>{{ entry.name }}</strong> trinkt {{ entry.variant }} –
          <span class="text-sm text-gray-500">vor {{ entry.timestamp }} Min</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const selectedVariant = ref('')
const checkIns = ref([
  { name: 'Nils', variant: 'Eierlikoer im Kaffee', timestamp: 2 },
  { name: 'Lisa', variant: 'Eierlikoer pur', timestamp: 5 }
])

function checkIn() {
  if (!selectedVariant.value) return
  checkIns.value.unshift({
    name: 'Du',
    variant: selectedVariant.value,
    timestamp: 0
  })
  selectedVariant.value = ''
}
</script>
