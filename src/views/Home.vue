<template>
  <main v-if="!loading">
    <Title :text="title" :dataDate="dataDate" />
    <Boxes :status="status" />
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

export default {
  name: 'Home',
  components: {
    Title,
    Boxes,   
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
