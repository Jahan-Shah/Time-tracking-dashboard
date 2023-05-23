<script setup>
import { ref } from "vue";
import TrackingItem from "./components/TrackingItem.vue";

const selectedDuration = ref("Week");
</script>

<template>
  <section>
    <div class="user">
      <div class="profile">
        <img src="/image-jeremy.png" alt="profile picture" />
        <p>Report for</p>
        <h1>Jeremy<br />Robson</h1>
      </div>
      <div class="filter">
        <input type="radio" id="daily" value="Day" v-model="selectedDuration" />
        <label for="daily">Daily</label>
        <input
          type="radio"
          id="weekly"
          value="Week"
          v-model="selectedDuration"
          checked
        />
        <label for="weekly">Weekly</label>
        <input
          type="radio"
          id="monthly"
          value="Month"
          v-model="selectedDuration"
        />
        <label for="monthly">Monthly</label>
      </div>
    </div>
    <TrackingItem :selected-duration="selectedDuration" />
  </section>
</template>

<style scoped>
h1 {
  font-size: 2.5rem;
  font-weight: var(--fw-reg);
}

img {
  width: 6rem;
  aspect-ratio: 1;
  border: 3px solid white;
  border-radius: 50%;
}

section {
  display: flex;
  gap: 30px;
}

.user {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 255px;
  overflow: hidden;
  border-radius: 0.8rem;
  background-color: var(--neutral-200);
}

.filter {
  display: flex;
  flex-direction: column;
}

.profile {
  padding: 32px 28px;
  padding-bottom: 76px;
  color: white;
  background-color: var(--clr-primary);
  border-radius: 0.8rem;
}

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
