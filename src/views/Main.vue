<script setup>
import AllStocks from '../components/AllStocks.vue'
import Chart from '../components/Chart.vue'
//информация о торгуемых акциях на Московской бирже
let url = 'https://iss.moex.com/iss/engines/stock/markets/shares/boards/'
let boardid = 'TQBR' //идентификатор режима торгов
url = 'https://iss.moex.com/iss/engines/stock/markets/shares/boards/' + boardid + '/securities.json?iss.meta=off&iss.only=securities&securities.columns=SECID,SECNAME'
</script>
<template>
    <AllStocks />
    <Chart />
</template>