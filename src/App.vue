<script setup>
import SplashScreen from "./components/SplashScreen.vue";
import {  defineAsyncComponent } from "vue";

const Home = defineAsyncComponent(() =>{
return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(import("./components/Home.vue"))
    }, 2500);
  })
})

</script>

<template>
  <Suspense>
    <template #default>
      <Home></Home>
    </template>
    <template #fallback>
      <SplashScreen></SplashScreen>
    </template>
  </Suspense>
</template>

<style>
  html,
  body,
  .app {
    min-height: 100vh;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }

  * {
    --brand-green: #04b500;
    --brand-blue: #0689b0;
  }
</style>
