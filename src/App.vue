<template>
  <!-- suspenses sirve para que un compoente con el atributo fallback se renderize primero hasta que nuestra pagina termine de cargar este desapareseria -->
  <Suspense>
    <template #default>
      <HomeCasaVue />
    </template>
    <template #fallback>
      <SplashScreenVue />
    </template>
  </Suspense>
</template>

<script>
import { defineAsyncComponent } from "vue";
import SplashScreenVue from "./components/Splash-screen.vue";

export default {
  name: "App",
  components: {
    SplashScreenVue,
    HomeCasaVue: defineAsyncComponent(
      () =>
        new Promise((resolve) => {
          setTimeout(() => {
            resolve(import("./components/Home-casa.vue"));
          }, 2500);
        })
    ),
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
