<template>
  <button
    class="px-3 py-1 text-sm font-medium border border-gray-200 rounded-full :hover:bg-gray-100"
    @click="$emit('click')"
  >
    {{ label }}
  </button>
</template>

<script setup>
defineEmits(['click']);
defineProps({
  label: String
});
</script>
