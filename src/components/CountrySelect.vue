<template>
  <select
    v-model="selected"
    class="form-select mt-10 block w-full border p-3 rounded"
    @change="onChange"
  >
    <option value="0">Select Country</option>
    <option v-for="country in countries" :value="country.ID" :key="country">
      {{ country.Country }}
    </option>
  </select>
</template>

<script setup>
import { ref, defineEmit } from 'vue';

const emit = defineEmit(['get-country'])
const props = defineProps(['countries'])
const selected = ref(0);

const onChange = () => {
  const country = props.countries.find((item) => item.ID === selected.value);
  emit('get-country', country);
}
</script>
