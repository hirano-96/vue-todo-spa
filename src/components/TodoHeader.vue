<script setup lang="ts">
// 親コンポーネントから渡されるものを定義する
defineProps({
  msg: {
    type: String,
    required: true // 渡されなくても良い設定
  }
})
</script>

<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>
</template>
