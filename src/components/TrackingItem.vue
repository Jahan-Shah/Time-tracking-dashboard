<script setup>
import { onMounted, ref } from "vue";

const jsonData = ref([]);

async function fetchData() {
  try {
    const response = await fetch("/data.json");
    jsonData.value = await response.json();
  } catch (error) {
    console.error("Error fetching data from JSON: ", error);
  }
}
onMounted(fetchData);

const getNameForClass = (item) => {
  const className =
    item.title.charAt(0).toLowerCase() + item.title.substring(1);
  return className.replace(/\s+/g, "");
};
</script>

<template>
  <div class="item__container">
    <div
      class="item__bg"
      :class="getNameForClass(item)"
      v-for="item in jsonData"
    >
      <img :src="`/icon-${getNameForClass(item)}.svg`" alt="" />
      <div class="item">
        <div class="heading">
          <h3>{{ item.title }}</h3>
          <img src="/icon-ellipsis.svg" alt="ellipsis" />
        </div>
        <h2>{{ item.timeframes.weekly.current }}hrs</h2>
        <p>Last Week - {{ item.timeframes.weekly.previous }}hrs</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.item__container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 30px;
}

.item__bg {
  width: 255px;
}

.item {
  color: white;
  background-color: var(--neutral-200);
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
