<template>
  <div class="product-card" @click="emit('show', product)">
    <img :src="product.image" :alt="`${product.name} image`" class="product-card-image" />
    <h3>{{ product.name }}</h3>
    <p>{{ product.priceRange }}</p>
  </div>
</template>

<script setup>
defineProps({ 
  product: {
    type: Object, 
    required: true 
  }
})

const emit = defineEmits(['show'])
</script>

<style scoped>
.product-card {
  cursor: pointer;
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 8px;
  width: 200px;
}

.product-card-image {
  max-width: 100%;
}

@media (max-width: 768px) {
  .product-card {
    width: 100%;
    max-width: 80vw;
  }
}
</style>
