<script setup>
import HeaderComp from "@/components/template/HeaderComp.vue";
</script>

<template>
  <HeaderComp />
  <RouterView />
  <footer>Rodapé</footer>
</template>

<style>
@import "@/assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  font-weight: normal;
  height: 100vh;
}

a {
  color: inherit;
  text-decoration: none;
}

header,
footer {
  height: 15%;
  padding-left: 2%;
  color: white;
  font-size: 1.3rem;
  background-color: rgb(59, 59, 127);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

header span {
  padding: 0 20px;
}

main {
  height: 70%;
}
</style>
