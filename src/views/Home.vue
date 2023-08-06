<template>
  <h1>Home Page</h1>
  <input class="input-search" type="text" v-model="nameValue" />
  <div v-for="name in computedValue" :key="name">
    <p>{{ name }}</p>
  </div>
  <button @click="handleClick">Stop Watching</button>
</template>

<script>
import { computed, ref, watch, watchEffect } from "vue";
export default {
  setup() {
    const nameValue = ref("");
    const names = ref([
      "chinedu",
      "chika",
      "chinazor",
      "bimbo",
      "abimbola",
      "seun",
    ]);

    const stopWatch = watch(nameValue, () => {
      console.log("watchEffect function", nameValue.value);
    });

    const stopEffect = watchEffect(() => {
      console.log("watchEffect function ran");
    }, nameValue.value);
    const computedValue = computed(() => {
      return names.value.filter((name) => name.includes(nameValue.value));
    });

    const handleClick = () => {
      stopWatch();
      stopEffect();
    };

    return { names, nameValue, computedValue, handleClick };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;700&family=Rubik:ital,wght@0,400;0,500;0,600;1,400&display=swap");
input[type="text"] {
  background: #ececec;
  height: 3em;
  width: 40%;
  text-indent: 8px;
  border: none;
  font-family: "Rubik", Courier, monospace;
  border-radius: 10px;
  font-size: 20px;
}
input:focus {
  outline: none;
  box-shadow: 0 0 0 0 8em rgba(0, 0, 0, 0.12);
}
</style>
