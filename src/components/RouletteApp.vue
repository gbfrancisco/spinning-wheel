<template>
  <div class="app-container">
    <div class="header-container row justify-center">
      <base-header message="Spin the Wheel" color="white" />
    </div>
    <div class="app-body row">
      <div class="wheel-container col justify-center">
        <the-wheel :height="525" :width="525" />
      </div>
      <div class="board-container col justify-center">
        <item-box />
      </div>
    </div>
  </div>
</template>

<script>
import BaseHeader from "./BaseHeader.vue";
import TheWheel from "./TheWheel.vue";
import ItemBox from "./ItemBox.vue";
export default {
  components: { BaseHeader, TheWheel, ItemBox },
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
.app-container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}
.header-container {
  background-color: $blue-9;
}
.app-body {
  flex-grow: 1;
  margin: 0px 200px;
}
.wheel-container {
  display: flex;
  align-items: center;
}
.board-container {
  display: flex;
  align-items: center;
}
</style>
