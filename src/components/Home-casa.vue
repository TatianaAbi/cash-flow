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
        <template #graphic>
          <GraphicMoneyVue :amounts="amounts" />
        </template>
        <template #action>
          <ActionBtnVue />
        </template>
      </IndexResumeVue>
    </template>

    <template #movements>
      <MovementsOneVue :movements="movements" />
    </template>
  </LayoutDeLogoVue>
</template>
<script>
import ActionBtnVue from "./ActionBtn.vue";
import HeaderSeccionVue from "./HeaderSeccion.vue";
import LayoutDeLogoVue from "./LayoutDeLogo.vue";
import MovementsOneVue from "./Movements/MovementsOne.vue";
import IndexResumeVue from "./ResumeWeb/IndexResume.vue";
import GraphicMoneyVue from "./ResumeWeb/GraphicMoney.vue";
export default {
  components: {
    ActionBtnVue,
    LayoutDeLogoVue,
    HeaderSeccionVue,
    MovementsOneVue,
    IndexResumeVue,
    GraphicMoneyVue,
  },
  data() {
    return {
      amount: null,
      amounts: [100, 200, 500, 200, -400, -600, -300, 0, 500],
      movements: [
        {
          id: 0,
          title: "Movimiento 1",
          description: "lorem ips is la sit met flo rui",
          amount: 1000,
        },
        {
          id: 1,
          title: "Movimiento 2",
          description: "lorem ips is la sit met flo rui",
          amount: 1000,
        },
        {
          id: 2,

          title: "Movimiento 3",
          description: "lorem ips is la sit met flo rui",
          amount: 1000,
        },
        {
          id: 3,
          title: "Movimiento 4",
          description: "lorem ips is la sit met flo rui",
          amount: 1000,
        },
      ],
    };
  },
};
</script>
