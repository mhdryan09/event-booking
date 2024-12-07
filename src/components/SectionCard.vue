<template>
  <RoundedCard>
    <h3 class="p-4 text-xl font-medium border-b border-gray-200">
      <slot name="header"></slot>
    </h3>

    <div class="p-4 border-b border-gray-200">
      <slot />
    </div>

    <div class="p-4">
      <slot name="footer"></slot>
    </div>
  </RoundedCard>
</template>

<script setup>
import RoundedCard from '@/components/RoundedCard.vue';
</script>
