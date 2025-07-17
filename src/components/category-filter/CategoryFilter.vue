<template>
  <div class="category-tree">
    <CategorySelector
      v-for="(category, i) in categories"
      :key="i"
      :category="category"
      :selected-categories="selectedCategories"
      @toggle="handleToggle"
    />
  </div>
</template>

<script setup>
import CategorySelector from '../category-filter/CategorySelector.vue'

const props = defineProps({
  categories: Array,
  selectedCategories: Array
})

const emit = defineEmits(['update:selected'])

function handleToggle(id) {
  emit('update:selected', id)
}
</script>

<style scoped>
.category-tree {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  position: sticky;
  top: 0;
  flex-shrink: 0;
  padding: 1rem;
}

@media (max-width: 768px) {
  .category-tree {
    position: relative;
  }
}
</style>
