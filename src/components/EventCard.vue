<template>
  <div class="bg-white border border-gray-200 rounded-md">
    <h3 class="p-4 text-xl font-medium border-b border-gray-200">{{ title }}</h3>
    <p class="p-4 border-b border-gray-200">{{ when }}</p>
    <p class="p-4">{{ description }}</p>

    <section class="flex justify-end p-4">
      <button
        class="px-3 py-1 text-sm font-medium border border-gray-200 rounded-full :hover:bg-gray-100"
        @click="$emit('register')"
      >
        Register
      </button>
    </section>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  when: String,
  description: String
});

defineEmits(['register']);
</script>
