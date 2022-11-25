<template>
  <q-card class="item-box-container text-white">
    <q-card-section>
      <div class="text-h5 text-center">List of Stuff</div>
    </q-card-section>

    <q-card-section class="item-box-items-container">
      <item v-for="(item, idx) in itemList" :key="idx" :itemName="item" />
    </q-card-section>

    <q-separator dark />

    <q-card-section class="item-box-actions-container flex justify-center">
      <q-input
        v-model="itemInput"
        bg-color="white"
        dense
        :input-style="{ fontWeight: '500' }"
        outlined
        placeholder="Item Name"
      />
      <q-btn class="bg-blue-7 q-pa-sm q-mx-sm" flat>Add Item</q-btn>
      <q-btn class="bg-blue-7 q-pa-sm" flat>Remove All</q-btn>
    </q-card-section>
  </q-card>
</template>

<script>
import Item from "./Item.vue";

export default {
  components: { Item },
  data() {
    return {
      itemInput: "",
      itemList: ["test", "test1", "test2"],
    };
  },
};
</script>

<style scoped lang="scss">
.item-box-container {
  display: flex;
  flex-direction: column;
  width: 420px;
  height: 600px;
  background-color: $blue-9;
}
.item-box-items-container {
  flex-grow: 1;
  background-color: $blue-3;
}
.item-box-title {
  color: white;
  font-size: 28px;
  padding: 10px;
}
.item-container {
  flex-grow: 1;
}
.item-input-container {
  display: flex;
  justify-content: center;
  padding: 40px 0px;
  min-width: 100%;
  background-color: $blue-10;
}

.item-input-container input {
  min-width: 70%;
  padding: 15px 10px;
}
</style>
