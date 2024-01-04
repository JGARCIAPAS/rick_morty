<script setup>
import { ref, watchEffect } from "vue";
import "../assets/styles/components/ResidentsData.css";
const props = defineProps({
  residents: Array,
});
const characters = ref([]);

const fetchCharsData = async () => {
  try {
    const request = props.residents.map(async (eachUrl) => {
      const response = await fetch(eachUrl);
      return response.json();
    });
    const responses = await Promise.all(request);
    characters.value = responses.map((response) => response);
    console.log(characters.value);
  } catch (error) {
    console.error("fetch error", error);
  }
};
watchEffect(() => {
  if (props.residents) {
    fetchCharsData();
  }
});
</script>
<template>
  <ul>
    <li v-for="character in characters" :key="character.id">
      <img :src="character.image" />
      <p class="character-data">{{ character.name }}</p>
      <p class="character-data">{{ character.status }}</p>
    </li>
  </ul>
</template>
