<template>
  <LayoutDeLogoVue>
    <template #header>
      <HeaderSeccionVue></HeaderSeccionVue>
    </template>
    <template #resume>
      <IndexResumeVue
        :label="'ahorro total'"
        :total-amount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <GraphicMoneyVue :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <ActionBtnVue @create="create" />
        </template>
      </IndexResumeVue>
    </template>

    <template #movements>
      <MovementsOneVue :movements="movements" @remove="remove" />
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
      movements: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);

          return m.time > oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);

        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, m) => {
        return suma + m.amount;
      }, 0);
    },
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));
    if (Array.isArray(movements)) {
      this.movements = movements?.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },
  methods: {
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
    select(el) {
      this.amount = el;
    },
  },
};
</script>
