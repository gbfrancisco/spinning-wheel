<template>
  <div class="app-container">
    <div class="header-container row justify-center">
      <base-header message="Spin the Wheel" color="white" />
    </div>
    <div class="row full-height">
      <div class="wheel-container col-7 justify-center">
        <the-wheel />
      </div>
      <div class="board-container col justify-center">Test2</div>
    </div>
  </div>
</template>

<script>
import BaseHeader from "./BaseHeader.vue";
import TheWheel from "./TheWheel.vue";
export default {
  components: { BaseHeader, TheWheel },
  data() {
    return {
      counter: 0,
    };
  },
  computed: {},
  methods: {},
};
</script>

<style scoped lang="scss">
.header-container {
  background-color: $info;
}
// .wheel-container {
// }
// .board-container {
// }
</style>
