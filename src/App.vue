<template>
  <div>
    <CascadeFromSelect
      v-model:selected-city="model.city"
      v-model:selected-sub-city="model.subCity"
      v-model:summary="model.summary"
    ></CascadeFromSelect>
    {{ model }}
  </div>
</template>

<script setup>
import { ref } from 'vue';
import CascadeFromSelect from '@/components/CascadeFromSelect.vue';

const model = ref({});
</script>
