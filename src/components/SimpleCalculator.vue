<template>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">
    <!--calculator result */ -->
    <div class="w-full rounded m-1 p-3 text-end lead font-weight bold text-white bg-vue-dark">
      {{ calculatorValue || 0 }}
    </div>

    <!--calculator buttons-->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorKeys" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{ 'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n) }"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SimpleCalculator",
  props: {
    msg: String,
  },

  data() {
    return {
      calculatorValue: "",
      calculatorKeys: ["C", "*", "/", "-", 7, 8, 9, "+", 4, 5, 6, "%", 1, 2, 3, "=", 0, "."],
    };
  },
};
</script>

<style scoped>
.bg-vue-dark {
  background: #31475e;
}
.hover-class:hover {
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green {
  background: #3fb984;
}
</style>
