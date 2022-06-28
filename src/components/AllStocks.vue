<script setup>
import { onMounted, ref, watch } from 'vue'
import axios from 'axios'

const urlToAllStocks = 'http://iss.moex.com/iss/engines/stock/markets/shares/boards/TQBR/securities.json?iss.meta=off&iss.only=securities&securities.columns=SECID,PREVADMITTEDQUOTE'

let priceOfAllStocks = ref([])
let tableData = ref([])

const columns = ref([{ title: 'Акция', dataIndex: 'ticker' }, { title: 'Цена', dataIndex: 'price' }])

function getDataAboutAllStocks() {
    axios.get(urlToAllStocks)
        .then((response) => {
            priceOfAllStocks.value = response.data.securities.data
            tableData.value = parseDataToTableData(priceOfAllStocks)
        })
}

function parseDataToTableData(data) {
    data = data.value
    let result = []

    for (let arr of data) {
        result.push({
            ticker: arr[0],
            price: arr[1],
        })
    }

    return result
}

onMounted(() => {
    getDataAboutAllStocks()
    setInterval(getDataAboutAllStocks, 10000)
})

</script>
<template>
    <a-typography-title style="margin-top: 8px">Текущие котировки акции</a-typography-title>
    <a-table :columns="columns" :data-source="tableData" :pagination="true" bordered>
    </a-table>
</template>