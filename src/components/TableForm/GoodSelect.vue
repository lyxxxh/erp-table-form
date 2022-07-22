<template>
<div>
    <el-select
        filterable
        remote
        ref="selectRef"
        :remote-method="remoteMethod"
        :loading="loading"
        @change="changeSelect"
        v-model="value"
        @keydown.tab.stop="tab" @keydown.enter.stop="enter"

    >
      <el-option
          v-for="item in goods"
          :key="item.id"
          :label="item.goods_name"
          :value="item.id"
      />
    </el-select>
    </div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from 'vue' 
const goods:any = ref([])
const loading = ref(false)
const emit = defineEmits(['selectedGood'])

const selectRef:any = ref(null)
const props = defineProps({
  index: {
    type: Number
  },
  goods_name: {
    type: String,
    default:() => ''
  }
})
const  value = ref('')

onMounted(() => {
    setTimeout(() => (selectRef.value.selectedLabel = props.goods_name))
})


// 搜索商品
const remoteMethod = async (query: string) => {
    loading.value = true
    goods.value = await mockSearchGoods(query)
    loading.value = false
}


// 选择商品
const changeSelect = (id:any) => {
    emit('selectedGood',{
    good: goods.value.find((good:any) => good.id === id),
    index:props.index
    })
}

// mock接口
const mockSearchGoods = async (query:string)  =>  new Promise(resolve => 
    setTimeout(() => 
        resolve(randData())
    ,500)
)

// 随机返回数据
const randData = () => [
    {'goods_name':'红牛','goods_bar_code':'69*****red','price':'2.00',id:1},
    {'goods_name':'黄牛','goods_bar_code':'69*****yellow','price':'3.00',id:2},
    {'goods_name':'蓝牛','goods_bar_code':'69*****blue','price':'4.00',id:3},
    {'goods_name':'*牛','goods_bar_code':'69*****','price':'5.00',id:4},
    {'goods_name':'*2','goods_bar_code':'69*****2','price':'6.00',id:5}
].sort(() => Math.random() - 0.5)

const tab = () => console.log('自定义tab键处理')
const enter = () => console.log('自定义enter键处理')

</script>
