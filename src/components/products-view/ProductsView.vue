<template>
  <div class="products-view">
    <CategoryFilter
      :categories="printCategories.children"
      :selected-categories="selectedCategories"
      @update:selected="toggleCategory"
    />

    <section class="products-list">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @show="selectedProduct = $event"
      />
    </section>

    <DetailsModal
      v-if="selectedProduct"
      :title="selectedProduct.name"
      :description="selectedProduct.description"
      :image="selectedProduct.image"
      :priceRange="selectedProduct.priceRange"
      @close="selectedProduct = null"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import printCategories from '../../mocks/printCategories'
import CategoryFilter from '../category-filter/CategoryFilter.vue'
import ProductCard from '../product-card/ProductCard.vue'
import DetailsModal from '../details-modal/DetailsModal.vue'

const selectedCategories = ref([])
const selectedProduct = ref(null)

const filteredProducts = computed(() =>
  getProductsBySelectedCategories(printCategories)
)

function toggleCategory(id) {
  const index = selectedCategories.value.indexOf(id)
  if (index > -1) {
    selectedCategories.value.splice(index, 1)
  } else {
    selectedCategories.value.push(id)
  }
}

function getProductsBySelectedCategories(categories) {
  let products = []

  if (categories.id && selectedCategories.value.includes(categories.id)) {
    products.push(categories)
  }

  if (categories.children) {
    categories.children.forEach(child => {
      products.push(...getProductsBySelectedCategories(child))
    })
  }

  return products
}
</script>

<style scoped>
.products-view {
  display: flex;
  gap: 2rem;
  padding: 2rem;
  align-items: flex-start;
}

.products-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  flex: 1;
}

@media (max-width: 768px) {
  .products-view {
    flex-direction: column;
    padding: 1rem;
  }

  .products-list {
    justify-content: center;
  }
}
</style>
