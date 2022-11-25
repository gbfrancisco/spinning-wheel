<template>
  <div class="item flex justify-between q-pa-sm">
    <div class="item-text text-h6">{{ itemName }}</div>
    <q-btn @click="handleRemoveItem" class="bg-primary">
      <q-icon name="clear" />
    </q-btn>
  </div>
</template>

<script>
export default {
  props: {
    itemName: {
      type: String,
      required: true,
    },
    itemIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    handleRemoveItem() {
      this.$emit("removeItem", this.itemIndex);
    },
  },
};
</script>

<style scoped lang="scss">
.item {
  background-color: $blue-10;
  border-radius: 7px;
}
.item-text {
  display: flex;
  align-items: center;
}
</style>
