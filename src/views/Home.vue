<template>
  <main v-if="!loading">
    <Title :text="title" :dataDate="dataDate" />
    <Boxes :status="status" />
    <countrySelect @get-country="getCountryData" :countries="countries" />
    <button v-if="status.Country" @click="clearData"
      class="bg-green-500 text-white rounded p-3 mt-10 focus:outline hover:bg-green-400">
      Clear Country
    </button>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
      <img :src="loadingImage" class="w-24 m-auto" alt="" />
    </div>
  </main>
</template>

<script>

import axios from 'axios';
import Title from "@/components/Title.vue";
import Boxes from '@/components/Boxes.vue';
import countrySelect from '@/components/countrySelect.vue';

export default {
  name: 'Home',
  components: {
    Title,
    Boxes,
    countrySelect,   
  },
  data()
  {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      status: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    }
  },
  methods: {
    async fetchData()
    {
      const res = await axios.get('https://api.covid19api.com/summary');
      const data = await res.data;
      return data;
    },
    getCountryData(country)
    {
      this.status = country;
      this.title = country.Country;
    },
    async clearData()
    {
      this.loading = true;
      const data = await this.fetchData();
      this.title = 'Global';
      this.status = data.Global;
      this.loading = false;      
    }
  },
  async created()
  {
    const data = await this.fetchData();
    this.dataDate = data.Date;
    this.status = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  }
  
}
</script>
