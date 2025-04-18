<script setup>
import ListItem from "@/components/ListItem.vue";
const props = defineProps({
  items: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <div class="list bordered">
    <template v-for="item in items" :key="item.id" >
      <ListItem :item="item" @chose="$emit('chose', item.id)"/>
    </template>

  </div>
</template>

<style scoped>

</style>