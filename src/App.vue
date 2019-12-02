<template>
  <div id="app">
    <CountUp class="CountUp" :num="num0"></CountUp>
    <CountUp class="CountUp" :num="num1"></CountUp>
  </div>
</template>

<script>
import CountUp from "./components/count-up";
export default {
  name: "app",
  components: {
    CountUp
  },
  data() {
    return {
      num0: 2010,
      num1: 666
    };
  }
};
</script>

<style lang="scss">
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
