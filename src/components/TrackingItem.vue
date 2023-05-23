<script setup>
import { onMounted, ref } from "vue";

const jsonData = ref([]);
const props = defineProps(["selectedDuration"]);

function getCurrentTime(item) {
  if (props.selectedDuration === "Day") return item.timeframes.daily.current;
  else if (props.selectedDuration === "Week")
    return item.timeframes.weekly.current;
  else if (props.selectedDuration === "Month")
    return item.timeframes.monthly.current;
}
function getPreviousTime(item) {
  if (props.selectedDuration === "Day") return item.timeframes.daily.previous;
  else if (props.selectedDuration === "Week")
    return item.timeframes.weekly.previous;
  else if (props.selectedDuration === "Month")
    return item.timeframes.monthly.previous;
}

async function fetchData() {
  try {
    const response = await fetch("/data.json");
    jsonData.value = await response.json();
  } catch (error) {
    console.error("Error fetching data from JSON: ", error);
  }
}
onMounted(fetchData);

const getTitle = (item) => {
  const className =
    item.title.charAt(0).toLowerCase() + item.title.substring(1);
  return className.replace(/\s+/g, "");
};
</script>

<template>
  <div class="item__container">
    <div class="item" :class="getTitle(item)" v-for="item in jsonData">
      <img
        class="item__svg"
        :src="`/icon-${getTitle(item)}.svg`"
        alt="tracking icon"
      />
      <div class="item__content">
        <div class="heading">
          <h3>{{ item.title }}</h3>
          <img src="/icon-ellipsis.svg" alt="ellipsis" />
        </div>
        <h2>{{ getCurrentTime(item) }}hrs</h2>
        <p>
          Last {{ props.selectedDuration }} - {{ getPreviousTime(item) }}hrs
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.item__container {
  max-width: 830px;
  display: grid;
  grid-template-columns: repeat(auto-fit, 255px);
  grid-gap: 30px;
}

.item {
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  position: relative;
  padding-top: 43px;
  overflow: hidden;
  border-radius: 0.8rem;
}

.item__svg {
  align-self: flex-end;
  width: fit-content;
  position: absolute;
  top: -5px;
  right: 16px;
}

.heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.item__content {
  padding: 20px 30px;
  color: white;
  background-color: var(--neutral-200);
  z-index: 1;

  border-radius: 0.8rem;
}

h3 {
  font-size: 1.125rem;
  font-weight: var(--fw-med);
}

h2 {
  padding-top: 1.6rem;
  font-size: 3.5rem;
  font-weight: var(--fw-reg);
}

p {
  font-weight: var(--fw-reg);
  font-size: 0.96rem;
  color: var(--neutral-400);
}

@media (max-width: 539px) {
  .item__container {
    padding: 1.5rem;
  }
  .item {
    width: 330px;
    grid-column: span 1;
  }
}

.work {
  background-color: var(--work);
}
.play {
  background-color: var(--play);
}
.study {
  background-color: var(--study);
}
.exercise {
  background-color: var(--exercise);
}
.social {
  background-color: var(--social);
}
.selfCare {
  background-color: var(--selfCare);
}
</style>
