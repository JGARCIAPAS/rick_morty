<script setup>
//import "../assets/styles/components/UniverseCard.css";
import { ref, onMounted } from "vue";
import LoadingSpinner from "./LoadingSpinner.vue";
const universes = ref([]);
const selectedLocationId = ref(null);
const urlLocation = ref("");
const loading = ref(true);
const fetchData = async () => {
  try {
    const response = await fetch("https://rickandmortyapi.com/api/location/");
    const data = await response.json();
    universes.value = data.results;
    console.log(universes);
  } catch (error) {
    console.error("fetch error", error);
  } finally {
    setTimeout(() => {
      //dont want to do this but ¯\_(ツ)_/¯
      loading.value = false;
    }, 1500);
  }
};

const fetchCharData = async (urlChar) => {
  try {
    const response = await fetch(urlChar);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("fetch error", error);
  }
};
onMounted(() => {
  fetchData();
});
</script>
<template>
  <LoadingSpinner v-if="loading" />
  <section class="card-location" v-else>
    <article v-for="location in universes" :key="location.id">
      <div class="top-data-location">
        <img
          class="earth"
          :title="location.name"
          :alt="location.name"
          src="/img/earth.png"
        />
        <div class="info-location">
          <p class="info-data-location">Name: {{ location.name }}</p>
          <p class="info-data-location">Type: {{ location.type }}</p>
          <p class="info-data-location">Created: {{ location.created }}</p>
          <p class="info-data-location">Dimension: {{ location.dimension }}</p>
          <p class="info-data-location">Id location: {{ location.id }}</p>
        </div>
      </div>
      <div class="bottom-data-location">
        <p>Residents</p>
        <div
          v-for="(resident, index) in location.residents"
          :key="index"
          @focus="fetchCharData(resident)"
        ></div>
      </div>
    </article>
  </section>
</template>
<!--       :created=""
  :dimension=""
  :id=""
  :name=""
  residents=""
  type=""
  url="" -->
