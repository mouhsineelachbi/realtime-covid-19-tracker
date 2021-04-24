<template>
    <select @change="onChange()"
        v-model="selected" class="form-select mt-10 block w-full border p-3 rounded">
        <option value="0">Select a country</option>
        <option v-for="country in countries" :value="country.ID">{{country.Country}}</option>
    </select>
</template>
<script>


export default {
    name: 'countrySelect',
    props: ['countries'],
    data ()
    {
        return {
            selected: 0,
        }
    },
    methods: {
        onChange()
        {
            const selectedCountry = this.countries.find((item)=> item.ID === this.selected)
            console.log(selectedCountry);

            // Emit selectedCoutry variable to other components
            this.$emit('get-country', selectedCountry);
        }
    }
}
</script>
