<template>
  <button
    :class="[
      'px-3 py-1 text-sm font-medium border border-gray-200 rounded-full :hover:bg-gray-100',
      variants[variant] ?? variants.default
    ]"
    @click="$emit('click')"
  >
    <slot></slot>
  </button>
</template>

<script setup>
const variants = {
  default: 'border border-gray-200 :hover:bg-gray-100',
  danger: 'bg-red-200 enabled:hover:bg-red-100 text-red-900'
};

defineProps({
  variant: {
    type: String,
    default: 'default'
  }
});
defineEmits(['click']);
</script>
