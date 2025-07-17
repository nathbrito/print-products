<template>
  <div class="modal-overlay" @click.self="emit('close')">
    <div class="modal" role="dialog" aria-modal="true">
      <img v-if="image" :src="image" :alt="`${title} image`" class="modal-image" />
      <h2 v-if="title">{{ title }}</h2>
      <p v-if="description">{{ description }}</p>
      <p v-if="priceRange">{{ priceRange }}</p>
      <button @click="emit('close')" class="close-button">Close</button>
    </div>
  </div>
</template>

<script setup>
defineProps({ 
  title: String, 
  description: String,
  image: String,
  priceRange: String
})

const emit = defineEmits(['close'])
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  max-width: 500px;
  width: 100%;
}

.modal-image {
  max-width: 100%;
}

.close-button {
  border-radius: 8px;
  border: none;
  padding: 0.6em 1.2em;
  font-size: 1em;
  cursor: pointer;
}
</style>
