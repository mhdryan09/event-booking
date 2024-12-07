<template>
  <SectionCard>
    <div class="flex justify-between">
      {{ title }}
      <RoundButton variant="danger">Cancel</RoundButton>
    </div>
  </SectionCard>
</template>

<script setup>
import RoundButton from './RoundButton.vue';
import SectionCard from './SectionCard.vue';

defineProps({
  title: String
});
</script>
