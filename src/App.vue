<template>
<TableFrom :columns="columns" :data="data" :isEdit="isEdit"/>
</template>

<script lang="ts" setup>
import TableFrom from './components/TableForm/index.vue'
import { onMounted, ref, getCurrentInstance } from 'vue';
const proxy = getCurrentInstance()
const columns = [
{field:'goods_name','type':'good_select','label':'商品'},
{field:'price','type':'number_input','label':'价格'},
{field:'goods_bar_code','type':'display','label':'条码'}
]

const data = ref([
    {'goods_name':'红牛','goods_bar_code':'69*****red','price':'2.00',minWidth:200},
    {'goods_name':'','goods_bar_code':'','price':'0.00',minWidth:200},
    {'goods_name':'','goods_bar_code':'','price':'0.00',minWidth:200},
    {'goods_name':'','goods_bar_code':'','price':'0.00',minWidth:200},
    {'goods_name':'','goods_bar_code':'','price':'0.00',minWidth:200},
    {'goods_name':'','goods_bar_code':'','price':'0.00',minWidth:200},
])
const isEdit = ref(true)

onMounted(() => {
    window.app = proxy 
    // 控制台调用:window.app.setupState.data 即可打印data
})
</script>