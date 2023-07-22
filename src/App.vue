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
    //nuestro componente home sera especial cuando el componente de carga se renderize el home se renderizara por atras por eso usamos una promesa
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
