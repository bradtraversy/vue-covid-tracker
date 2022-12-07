<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mt-4 mb-10">
      {{ timestamp(dataDate) }}
    </div>
  </div>
</template>

<script setup>
import dayjs from 'dayjs';

const props = defineProps(['text', 'dataDate'])

const timestamp = (dataDate) => (dayjs(dataDate).format('MMMM D YYYY, h:mm:ss a'))

</script>
