<template>
  <SectionCard>
    <div class="flex justify-between">
      <div class="flex space-x-3">
        <div>{{ title }}</div>
        <div>{{ status }}</div>
      </div>
      <RoundButton variant="danger" @click="$emit('cancelled')">Cancel</RoundButton>
    </div>
  </SectionCard>
</template>

<script setup>
import RoundButton from './RoundButton.vue';
import SectionCard from './SectionCard.vue';

defineProps({
  title: String,
  status: String
});

defineEmits(['cancelled']);
</script>
