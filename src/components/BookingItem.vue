<template>
  <SectionCard>
    <div class="flex justify-between">
      <div class="flex space-x-3">
        <div>{{ title }}</div>
        <div>
          <component :is="icon" :class="{ 'animate-spin': pending }" />
        </div>
      </div>
      <RoundButton variant="danger" @click="$emit('cancelled')">Cancel</RoundButton>
    </div>
  </SectionCard>
</template>

<script setup>
import { computed } from 'vue';
import RoundButton from './RoundButton.vue';
import SectionCard from './SectionCard.vue';
import { LoaderCircle, Check } from 'lucide-vue-next';

// untuk mengakses props, maka kita perlu bungkus dia ke dalam variabel
const props = defineProps({
  title: String,
  status: String
});

const pending = computed(() => props.status === 'pending');
const icon = computed(() => (pending.value ? LoaderCircle : Check));

defineEmits(['cancelled']);
</script>
