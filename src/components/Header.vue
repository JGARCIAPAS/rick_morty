<script setup>
import "./../assets/styles/components/Header.css";
defineProps({
  title: String,
});
</script>
<template>
  <header class="header">
    <picture>
      <source srcSet="./img/logo.svg" media="(min-width: 600px)" />
      <source srcSet="./img/logo-xs.svg" media="(max-width: 600px)" />
      <img class="main-logo" src="./img/logo.svg" />
    </picture>
    <h1>{{ title }}</h1>
  </header>
</template>
