<!-- <template>
  <div class="home">
    <SimpleCalculator></SimpleCalculator>

    <div v-for="calculation in calculations" v-bind:key="calculation.id"> -->
<!-- <h2>{{ calculation.value1 }}</h2>
    </div> -->
<!-- </div>
</template> -->
-->

<!-- <script>
// @ is an alias to /src
import SimpleCalculator from "@/components/SimpleCalculator.vue";
// import axios from "axios"; -->

<!-- export default {
  name: "HomeView",
  components: {
    SimpleCalculator, -->
<!-- },
  // data: function () {
  //   return {
  //     message: "",
  //     calculations: [],
  //   };
  // }, -->
<!-- // methods: {
  //   historyLog: function () {
  //   axios.get("http://localhost:3000/calculations.json").then((response) => {
  //     this.calculations = response.data;
  //     console.log("Calculations", this.calculations);
  //   });
  // },
};
</script> -->

<template>
  <div class="p-3" style="max-width: 400px; margin: 10px auto; background: lightblue">
    <!--calculator result */ -->
    <div class="w-full rounded m-1 p-3 text-end lead font-weight bold text-white bg-secondary">
      {{ calculatorValue || 0 }}
    </div>

    <!--calculator buttons-->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorKeys" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{ 'bg-vue-green': ['C', '+/-', '%', '/', '*', '-', '+', '='].includes(n) }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
  <div>
    <div class="container">
      <table class="table table-bordered">
        <thead class="thead-light">
          <!-- <tr>
            <th scope="col">History</th>
          </tr> -->
        </thead>
        <tbody>
          <tr v-for="calculation in calculations" v-bind:key="calculation.id">
            <td>{{ calculation.value1 }}</td>
            <td>{{ calculation.operator }}</td>
            <td>{{ calculation.value2 }}</td>
            <td>{{ calculation.equals }}</td>
            <td>{{ calculation.result }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SimpleCalculator",
  props: {
    msg: String,
  },

  data() {
    return {
      calculatorValue: "",
      calculatorKeys: ["C", "+/-", "%", "/", 7, 8, 9, "*", 4, 5, 6, "-", 1, 2, 3, "+", 0, ".", "history", "="],
      calculations: [],
    };
  },
  methods: {
    action(n) {
      /* assign value */
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }
      /* clear value */
      if (n === "C") {
        this.calculatorValue = "";
      }
      /* percent */
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }
      /* negative */
      if (n === "+/-") {
        this.calculatorValue = this.calculatorValue * -1;
      }

      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      if (n === "=") {
        this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue);

        this.previousCalculatorValue = "";
        this.operator = null;
      }
      if (n === "history")
        axios.get("http://localhost:3000/calculations.json").then((response) => {
          this.calculations = response.data;
          console.log("Calculations", this.calculations);
        });
    },
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
