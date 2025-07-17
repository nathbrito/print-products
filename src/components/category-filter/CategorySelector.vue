<template>
  <div class="category-node">
    <label v-if="showCategorySelector">
      <input type="checkbox" :checked="selected" @change="toggle" />
      {{ category.name }}
    </label>

    <div v-else>
      <div class="category-name">{{ category.name }}</div>
      <div class="child-nodes" v-if="category.children">
        <CategorySelector
          v-for="(child, i) in category.children"
          :key="i"
          :category="child"
          :selected-categories="selectedCategories"
          @toggle="emit('toggle', $event)"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import CategorySelector from './CategorySelector.vue'

const props = defineProps({
  category: Object,
  selectedCategories: Array
})

const emit = defineEmits(['toggle'])

const showCategorySelector = computed(() => !!props.category.id)
const selected = computed(() => props.selectedCategories.includes(props.category.id))

function toggle() {
  emit('toggle', props.category.id)
}
</script>

<style scoped>
.category-node {
  text-align: left;
}

.category-name {
  font-size: 22px;
  font-weight: 700;
}

.child-nodes {
  margin-left: 1rem;
}

.child-nodes .category-name {
  font-size: 18px;
  font-weight: 600;
}
</style>
