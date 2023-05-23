<script setup>
import { ref } from "vue";
import TrackingItem from "./components/TrackingItem.vue";

const selectedDuration = ref("Day");
</script>

<template>
  <input
    type="radio"
    id="daily"
    value="Day"
    name="duration"
    v-model="selectedDuration"
    checked
  />
  <label for="daily">Daily</label>
  <input
    type="radio"
    id="weekly"
    value="Week"
    name="duration"
    v-model="selectedDuration"
  />
  <label for="weekly">Weekly</label>
  <input
    type="radio"
    id="monthly"
    value="Month"
    name="duration"
    v-model="selectedDuration"
  />
  <label for="monthly">Monthly</label>
  <TrackingItem :selected-duration="selectedDuration" />
</template>

<style scoped>
input[type="radio"] {
  display: none; /* Hide the actual radio button */
}

label {
  color: white;
  display: inline-block;
  cursor: pointer;
}

input[type="radio"]:checked + label {
  text-decoration: underline;
}
</style>
