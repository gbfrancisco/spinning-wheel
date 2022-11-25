<template>
  <q-card class="item-box-container text-white">
    <q-card-section>
      <div class="text-h5 text-center">List of Stuff</div>
    </q-card-section>

    <q-card-section class="item-box-items-container">
      <item
        v-for="(item, idx) in filteredItemList"
        @remove-item="handleRemoveItem"
        :key="item"
        :itemIndex="idx"
        :itemName="item"
        class="item-element"
      />
    </q-card-section>

    <q-separator dark />

    <q-card-section class="item-box-actions-container flex justify-center">
      <q-input
        v-model="itemInput"
        @keydown.enter.prevent="addItem(itemInput)"
        bg-color="white"
        dense
        :input-style="{ fontWeight: '500' }"
        outlined
        placeholder="Item Name"
      />
      <q-btn
        @click.prevent="addItem(itemInput)"
        class="bg-blue-7 q-pa-sm q-mx-sm"
        flat
      >
        Add Item
      </q-btn>
      <q-btn @click.prevent="removeAllListItems" class="bg-blue-7 q-pa-sm" flat>
        Remove All
      </q-btn>
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
      itemList: [],
    };
  },
  computed: {
    filteredItemList() {
      return [...new Set(this.itemList)];
    },
  },
  methods: {
    addItem(itemName) {
      if (itemName) {
        this.itemList = this.filterDuplicates([...this.itemList, itemName]);
        this.itemInput = "";
      }
    },
    filterDuplicates(arr) {
      return [...new Set(arr)];
    },
    removeAllListItems() {
      this.itemList = [];
    },
    handleRemoveItem(index) {
      this.itemList.splice(index, 1);
    },
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
.item-element:not(:last-child) {
  margin-bottom: 10px;
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
