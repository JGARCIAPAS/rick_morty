<script setup>
import { ref, defineProps, defineEmits, watchEffect } from "vue";
import "../assets/styles/components/ModalLocation.css";
import ResidentsData from "./ResidentsData.vue";
const props = defineProps({
  isOpen: Boolean,
  urlLocation: String,
});

const emit = defineEmits(["closeModal"]);

const locationData = ref("");

const fetchLocationData = async () => {
  try {
    const response = await fetch(props.urlLocation);
    const data = await response.json();
    locationData.value = data;
    console.log(locationData.value);
  } catch (error) {
    console.error("fetch error", error);
  }
};
watchEffect(() => {
  if (props.urlLocation) {
    fetchLocationData();
  }
});
</script>
<template>
  <div v-if="isOpen" class="modal-background">
    <div class="modal-content">
      <div class="modal-header">
        <p>Wubba lubba dub dub!</p>
        <p @click="emit('closeModal')">
          <i class="fa-regular fa-circle-xmark"></i>
        </p>
      </div>
      <div class="modal-body">
        <p>Name: {{ locationData.name }}</p>
        <p>Type:{{ locationData.type }}</p>
        <p>Dimension: {{ locationData.dimension }}</p>
        <p class="residents-title">Residents</p>
        <ResidentsData :residents="locationData.residents" />
      </div>
    </div>
  </div>
</template>
