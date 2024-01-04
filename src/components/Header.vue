<script setup>
import "./../assets/styles/components/Header.css";
import logo from "../assets/img/logo.svg";
import logoXS from "../assets/img/logo-xs.svg";
defineProps({
  title: String,
});
</script>
<template>
  <header class="header">
    <picture>
      <source :srcSet="logo" media="(min-width: 600px)" />
      <source :srcSet="logoXS" media="(max-width: 600px)" />
      <img class="main-logo" :src="logo" />
    </picture>
    <h1>{{ title }}</h1>
  </header>
</template>
