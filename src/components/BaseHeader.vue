<template>
  <div :style="headerStyle">{{ message }}</div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    },
    color: {
      type: String,
      default: "black",
    },
    fontSize: {
      type: Number,
      default: 36,
    },
    width: {
      type: [Number, String],
      default: "fit-content",
    },
    height: {
      type: [Number, String],
      default: "fit-content",
    },
  },
  computed: {
    headerStyle() {
      return {
        width: this.width,
        height: this.height,
        color: this.color,
        fontSize: this.fontSize + "px",
      };
    },
  },
};
</script>
