<template>
<h3>{{ str }}</h3>
</template>

<script setup lang="ts">
defineProps({
  str:{
    type: String,
    default:() => ''
  }
})
</script>