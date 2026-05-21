<script setup>
import { ref, computed } from 'vue'

const armeSelectionnee = ref('M252')
const obusSelectionne = ref('')

const munitionsParArme = {
  'M252': [
    { name: 'HE', description: 'High Explosive', damage: 100, blastRadius: 5, weight: 4.06, speed: 243 },
  ],
  '2Б14': [
    { name: 'HE', description: 'High Explosive', damage: 100, blastRadius: 5, weight: 6.35, speed: 243 },
  ]
}

const obusDisponibles = computed(() => {
  return munitionsParArme[armeSelectionnee.value] || []
})

const obusDetails = computed(() => {
  return obusDisponibles.value.find(obus => obus.name === obusSelectionne.value)
})
</script>

<template>
  <h1>Arma Reforger Calculator</h1>
  <h2>Calculateur pour tir pour M252 et 2Б14</h2>

  <label for="arme">Arme :</label>
  <select id="arme" v-model="armeSelectionnee">
    <option value="M252">M252</option>
    <option value="2Б14">2Б14</option>
  </select>

  <br /><br />

  <label for="obus">Obus :</label>
  <select id="obus" v-model="obusSelectionne">
    <option disabled value="">Choisir un obus</option>
    <option
      v-for="obus in obusDisponibles"
      :key="obus.name"
      :value="obus.name"
    >
      {{ obus.name }}
    </option>
  </select>
</template>