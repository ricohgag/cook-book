<script lang="ts" setup>
import axios from 'axios';
import { ref } from 'vue';
import { Food } from '../api/cook-book/types.ts';

const foodsRef = ref<Food[]>([])

axios.get('/food/page')
  .then(resp => {
    console.log(resp);
    let foods: Food[] = resp.data.data;
    foodsRef.value = foods;
    console.log(foodsRef.value);
  })
  .catch(function (error) {
    console.log(error);
  });
</script>

<!-- MenuList.vue -->
<template>
  <div>
    <h2>Menu List</h2>
    <ul>
      <li v-for="menuItem in foodsRef" :key="menuItem.id">
        {{ menuItem.name }}
      </li>
    </ul>
  </div>
</template>



<style scoped>
/* 可以添加一些样式来美化菜单列表 */
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin-bottom: 8px;
  cursor: pointer;
}
</style>
