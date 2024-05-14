<template>
  <div class="card flex justify-content-center">
    <Dropdown
      v-model="selectedCity"
      :options="cities"
      optionLabel="name"
      optionValue="code"
      placeholder="選擇父項目"
      class="w-full md:w-14rem"
      showClear
      filter
      @change="onCityChange"
    />
    <Dropdown
      v-model="selectedSubCity"
      :options="subCities"
      optionLabel="name"
      optionValue="id"
      placeholder="選擇子項目"
      class="w-full md:w-14rem"
      :loading="onLoading"
      filter
      showClear
    />
    <InputText type="text" v-model="summary" />
  </div>
</template>

<script setup>
import { ref, defineModel } from 'vue';
const cities = ref([
  { name: 'New York', code: 'NY' },
  { name: 'Rome', code: 'RM' },
  { name: 'London', code: 'LDN' },
  { name: 'Istanbul', code: 'IST' },
  { name: 'Paris', code: 'PRS' },
]);
const subCities = ref([]);
const subCitiesSource = [
  { id: 1, code: 'NY', name: 'sub New York1' },
  { id: 2, code: 'NY', name: 'sub New York2' },
  { id: 3, code: 'RM', name: 'sub Rome' },
  { id: 4, code: 'LDN', name: 'sub London' },
  { id: 5, code: 'IST', name: 'sub Istanbul' },
  { id: 6, code: 'PRS', name: 'sub Paris' },
];

const selectedCity = defineModel('selectedCity');
const selectedSubCity = defineModel('selectedSubCity');
const summary = defineModel('summary');

const onLoading = ref(false);
const onCityChange = (event) => {
  if (event.value) {
    const subCitiesData = subCitiesSource.filter(
      (city) => city.code === event.value
    );
    subCities.value = subCitiesData;
    if (event.value !== selectedCity.value) selectedSubCity.value = null;
    onLoading.value = true;
    setTimeout(() => {
      onLoading.value = false;
    }, 400);
  } else {
    subCities.value = [];
    selectedSubCity.value = null;
  }
};
</script>
