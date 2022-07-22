<template>
<!-- 之所以不用el-input 忘记了 印象有坑就不用了 用css美化下input就好了-->
<input ref="inputRef" :value="modelValue"  @input="oninput"
@keydown.tab.stop="tab" @keydown.enter.stop="enter" @blur="blurHandle">
</template>

<script setup lang="ts">
import { defineProps, nextTick, onMounted, ref, defineEmits } from 'vue'

const emit = defineEmits(['update:modelValue', 'enterTab'])
const oninput = (e: any) => emit('update:modelValue', e.target.value)

const props: any = defineProps({
  modelValue: {}
})

const inputRef: any = ref(null)
onMounted(() =>
  nextTick(() => {
    inputRef.value.focus() // 聚焦
    inputRef.value.select() // 全选
  })
)


// 丢失焦点处理价格
const blurHandle = (e: any) => {
    const price = e.target.value

    if( false) // 价格不是数字之类的
    emit('update:modelValue', '0.00')
    emit('update:modelValue',parseFloat(price).toFixed(2)) 
    // emit('update:modelValue', )
}


const tab = () => console.log('自定义tab键处理')
const enter = () => console.log('自定义enter键处理')

</script>
