<template>
  <div class="home">
    <SimpleCalculator></SimpleCalculator>
  </div>
</template>

<script>
// @ is an alias to /src
import SimpleCalculator from "@/components/SimpleCalculator.vue";

export default {
  name: "HomeView",
  components: {
    SimpleCalculator,
  },
};
</script>
