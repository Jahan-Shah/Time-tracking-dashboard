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
        <div class="username">
          <p>Report for</p>
          <h1>Jeremy Robson</h1>
        </div>
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
  line-height: 1.2;
  font-size: 2.5rem;
  font-weight: var(--fw-reg);
}

img {
  height: 6rem;
  aspect-ratio: 1;
  border: 3px solid white;
  border-radius: 50%;
}

section {
  display: flex;
  gap: 30px;
}

p {
  font-size: 1rem;
  color: var(--neutral-400);
  padding-top: 2.6rem;
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
  height: 100%;
  padding: 22px 34px 32px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.profile {
  padding: 32px 28px 20%;
  color: white;
  background-color: var(--clr-primary);
  border-radius: 0.8rem;
}

input[type="radio"] {
  display: none; /* Hide the actual radio button */
}

label {
  color: var(--neutral-300);
  display: inline-block;
  cursor: pointer;
}

input[type="radio"]:is(:hover, :checked) + label {
  color: white;
}

@media (max-width: 539px) {
  h1 {
    font-size: 1.5rem;
  }
  section {
    margin-top: 2rem;
    display: grid;
    place-items: center;
    grid-template-columns: 1fr;
  }
  .user {
    width: 325px;
  }

  .profile {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1rem;

    padding: 32px 28px;
  }
  .username {
    display: block;
  }

  img {
    height: 4rem;
  }

  p {
    padding: 0;
  }

  .item__container {
    grid-template-columns: 1fr;
  }

  .filter {
    flex-direction: row;
    padding: 22px 34px;
  }
}
</style>
