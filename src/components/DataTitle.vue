<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mt-4 mb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs';
import { computed } from 'vue';

export default {
  name: 'DataTitle',
  props: ['text', 'dataDate'],
  setup ({ dataDate }) {
    return {
      timestamp: computed(() => dayjs(dataDate)
        .format('MMMM D YYYY, h:mm:ss a'))
    };
  }
};
</script>
