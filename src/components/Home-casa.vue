<template>
  <LayoutDeLogoVue>
    <template #header>
      <HeaderSeccionVue></HeaderSeccionVue>
    </template>
    <template #resume>
      <IndexResumeVue
        :label="'ahorro total'"
        :total-amount="100000"
        :amount="amount"
      >
        <template #graphic> graphic </template>
        <template #action> action </template>
      </IndexResumeVue>
    </template>

    <template #movements>
      <MovementsOneVue />
    </template>
  </LayoutDeLogoVue>
</template>
<script>
//import Resume from "./Resume/Index1.vue";
import HeaderSeccionVue from "./HeaderSeccion.vue";
import LayoutDeLogoVue from "./LayoutDeLogo.vue";
import MovementsOneVue from "./MovementsOne.vue";
import IndexResumeVue from "./ResumeWeb/IndexResume.vue";

export default {
  components: {
    LayoutDeLogoVue,
    HeaderSeccionVue,
    MovementsOneVue,
    IndexResumeVue,
  },
  data() {
    return {
      amount: null,
    };
  },
};
</script>
