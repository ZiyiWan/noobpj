<template>
   <pre>{{ jsonData }}</pre>
</template>
  
  <script setup>
  import {ref,  onMounted } from 'vue'
  import axios from 'axios'
  
  const jsonData = ref()

  // 独立数据获取函数
  const fetchData = async (functionUrl) => {
    try {
      const response = await axios.get(functionUrl)
      jsonData.value = response.data
    } catch (error) {
      console.error('获取数据时出错:', error)
    }
  }
  
  onMounted(() => {
    fetchData('https://getusers-o2v7rvex2q-uc.a.run.app')
  })
  </script>
  
  <style scoped>
  /* Customize styles as needed */
  </style>