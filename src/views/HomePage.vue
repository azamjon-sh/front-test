<script setup>
import {ref} from "vue";
import {useCollectionStore} from "@/stores/collection.js";
import ListComponent from "@/components/ListComponent.vue";
import ListItem from "@/components/ListItem.vue";

const collection = useCollectionStore()

const leftSelected = ref([])
const rightSelected = ref(null)

const maxSelected = ref(6)

const choseLeft = (id) => {
  const index = leftSelected.value.findIndex((e) => e.id === id);
  if (index !== -1) {
    leftSelected.value.splice(index, 1);
  } else if (leftSelected.value.length < maxSelected.value) {
    leftSelected.value.push(collection.leftCollection.find((e) => e.id === id));
  }
}
const choseRight = (id) => {
  if (rightSelected.value && rightSelected.value.id === id) {
    rightSelected.value = null
  } else {
    rightSelected.value = collection.rightCollection.find((e) => e.id === id)
  }
}
</script>

<template>
  <main class="main">
    <div class="top-grid">
      <div class="left-choose bordered">
        <template v-if="leftSelected.length">
          <ListItem v-for="item in leftSelected" :key="item.id" :item="item" @chose="choseLeft"/>
        </template>
        <div class="left-choose-count">
          {{ leftSelected.length }} / {{ maxSelected }}
        </div>
      </div>

      <ListItem class="right-choose" v-if="rightSelected" :item="rightSelected" @chose="choseRight"/>
    </div>
    <div class="bottom-grid">
      <ListComponent v-if="collection.leftCollection.length" @chose="choseLeft" :items="collection.leftCollection"/>
      <ListComponent v-if="collection.rightCollection.length" @chose="choseRight" :items="collection.rightCollection"/>
    </div>
  </main>

</template>

<style scoped>

</style>