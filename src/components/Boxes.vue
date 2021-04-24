<template>
    <div class="grid md:grid-cols-2 gap-4">
        <!-- Box 1 -->
        <div class="shadow-md bg-green-100 p10 text-center rounded">
            <h3 class="text-3xl text-green-800 font-bold mb-4">
                CASES
            </h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">New : </span>
                {{ formatNumber(status.NewConfirmed) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total : </span>
                {{ formatNumber(status.TotalConfirmed) }}
            </div>
        </div>
        <!-- Box 2 -->
        <div class="shadow-md bg-red-100 p10 text-center rounded">
            <h3 class="text-3xl text-green-800 font-bold mb-4">
                Deaths
            </h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">New : </span>
                {{ formatNumber(status.NewDeaths) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total : </span>
                {{ formatNumber(status.TotalDeaths) }}
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Boxes',
    props: ['status'],
    methods: {
        formatNumber(num) {
            return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
        },
    },

}
</script>
