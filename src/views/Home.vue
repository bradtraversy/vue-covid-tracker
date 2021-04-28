<template>
  <main v-if="!loading">
    <DataTitle :dataDate="dataDate" :text="title" />

    <DataBoxes :stats="status" />

    <CountrySelect :countries="countries" @get-country="getCountryData" />

    <button
      v-if="status.Country"
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
      @click="clearCountryData"
    >
      Clear Country
    </button>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="require('../assets/hourglass.gif')" alt="" class="w-24 m-auto" />
  </main>
</template>

<script>
import CountrySelect from '@/components/CountrySelect';
import DataBoxes from '@/components/DataBoxes';
import DataTitle from '@/components/DataTitle';
import { ref } from 'vue';

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  setup () {
    const loading = ref(true);
    const title = ref('Global');
    const dataDate = ref('');
    const status = ref({});
    const countries = ref([]);

    const fetchCovidData = async () => {
      const res = await fetch('https://api.covid19api.com/summary');
      return await res.json();
    };

    const getCountryData = (country) => {
      status.value = country;
      title.value = country.Country;
    };

    const clearCountryData = async () => {
      loading.value = true;
      const data = await fetchCovidData();
      title.value = 'Global';
      status.value = data.Global;
      loading.value = false;
    };

    const baseSetup = async () => {
      const data = await fetchCovidData();

      dataDate.value = data.Date;
      status.value = data.Global;
      countries.value = data.Countries;
      loading.value = false;
    };

    baseSetup();

    return {
      loading,
      title,
      dataDate,
      status,
      countries,
      getCountryData,
      clearCountryData
    };
  }
};
</script>
