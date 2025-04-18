<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true,
  }
})
</script>

<template>
  <div class="list-item bordered" @click="$emit('chose', item.id)">
    {{ item.name }}
  </div>
</template>

<style scoped>

</style>