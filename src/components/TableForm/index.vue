<template>
<el-table :cell-style="{ textAlign: 'center' }" @cell-click="cellClick" :data="data">
        <el-table-column v-for="column in columns" :key="column.field" :label="column.label" :min-width="column.minWidth">
          <template #default="scope">
            <!-- 表单处于不可编辑 或 字段本身就不可编辑 使用显示文本的组件 -->
            <Display v-if="! isEdit || column.type === 'display'" 
            :str="scope.row[`${column.field}`]"/>

        <GoodSelect v-if="column.type === 'good_select'" :goods_name="scope.row[`${column.field}`]" 
        :index="scope.$index"   @selectedGood="selectedGood"/>

        <NumberInput v-if="column.type === 'number_input'" :goods_name="scope.row[`${column.field}`]" 
        :index="scope.$index" v-model="scope.row[`${column.field}`]"/> 

          </template>
        </el-table-column>
      </el-table>
</template>

<script setup lang="ts">
import Display from './Display.vue'
import GoodSelect from './GoodSelect.vue'
import NumberInput from './NumberInput.vue'

const props = defineProps({
  columns: { // 列
    type: Object,
    required: true,
    default: () => {}
  },
  data: { // 数据
    type: Array,
    required: true,
    default: () => []
  },
  isEdit: { // 是否可编辑
    type: Boolean,
    default: () => true
  }
})


const cellClick = () => {

}

// 商品选择
const selectedGood = (data:any) => {
   props.data[data.index] = data.good
}


</script>
<style scoped lang="scss">

:deep(.cell) {
  text-align: center;
}
</style>