<script setup>
import ModalLocation from "./ModalLocation.vue";
import "../assets/styles/components/Universes.css";
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
onMounted(() => {
  fetchData();
});

const showModal = ref(false);
const openModal = (numberLocation, urlFetchLocation) => {
  showModal.value = true;
  selectedLocationId.value = numberLocation;
  urlLocation.value = urlFetchLocation;
};
const closeModal = () => {
  showModal.value = false;
};
</script>
<template>
  <LoadingSpinner v-if="loading" />
  <section v-else>
    <article
      v-for="location in universes"
      :key="location.id"
      @click="openModal(location.id, location.url)"
    >
      <img
        class="earth"
        :title="location.name"
        :alt="location.name"
        src="/img/earth.png"
      />
      <p>{{ location.name }}</p>
      <p>{{ location.type }}</p>
    </article>
    <ModalLocation
      :isOpen="showModal"
      :urlLocation="urlLocation"
      @closeModal="closeModal"
    />
  </section>
</template>
