<template>
  <q-card class="item-box-container text-white">
    <q-card-section>
      <div v-if="spinButtonVisibility === 0" class="text-h5 text-center">
        Add items
      </div>
      <div v-if="spinButtonVisibility === 1" class="text-h5 text-center">
        Add 1 more item
      </div>
      <div v-if="spinButtonVisibility === 2" class="text-h5 text-center">
        <q-btn class="text-h6 bg-primary">SPIN!</q-btn>
      </div>
    </q-card-section>

    <q-card-section class="item-box-items-container">
      <div
        v-for="(item, idx) in filteredItemList"
        :key="item"
        ref="itemRef"
        class="item-ref"
      >
        <item
          @remove-item="handleRemoveItem"
          :itemIndex="idx"
          :itemName="item"
          class="item-element"
        />
      </div>
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
import { nextTick } from "@vue/runtime-core";
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
    spinButtonVisibility() {
      const length = this.filteredItemList.length;

      // 0 - enable spin button
      if (length >= 2) {
        return 2;
      }

      // 1 - add one more item
      if (length === 1) {
        return 1;
      }

      // 2 - add items
      if (length === 0) {
        return 0;
      }
    },
  },
  methods: {
    async addItem(itemName) {
      if (itemName) {
        // get length before adding item for comparison later
        const initialLength = this.itemList.length;
        this.itemList = this.filterDuplicates([...this.itemList, itemName]);
        const newLength = this.itemList.length;

        // clear input
        this.itemInput = "";

        // only do logic below if an item has been added
        if (initialLength !== newLength) {
          await nextTick();
          this.$refs.itemRef[newLength - 1].scrollIntoView();
          this.$emit("added-item", this.itemList);
        }
      }
    },
    filterDuplicates(arr) {
      return [...new Set(arr)];
    },
    removeAllListItems() {
      this.itemList = [];
      this.$emit("removed-all-items", this.itemList);
    },
    handleRemoveItem(index) {
      // Used filter instead of splice due to weird behavior
      this.itemList = this.itemList.filter(
        (e) => this.itemList.indexOf(e) !== index
      );
      this.$emit("removed-item", this.itemList);
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
  background-color: $blue-3;
  flex-grow: 1;
  overflow-y: auto;
}
.item-box-title {
  color: white;
  font-size: 28px;
  padding: 10px;
}
.item-container {
  flex-grow: 1;
}
.item-ref:not(:last-child) {
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
