<script setup lang="ts" name="Demo">
import {ref} from "vue";
import axios from "axios";
import type {Food} from "@/api/food/types";

const value = ref('');

const onSearch = (name: string) => {
  getFoods(name)
};

const onCancel = () => {
  console.log('cancel');
};


const foodsRef = ref<Food[]>([])

// 根据菜品名搜索菜品
const getFoods = async (name: string) => {
  const {data} = await axios.get('/food/page', {
    params: {
      name,
    }
  })
  foodsRef.value = data.data;
}

getFoods('');
</script>

<template>
  <form action="/">
    <van-search
        v-model="value"
        show-action
        placeholder="请输入搜索关键词"
        @search="onSearch"
        @cancel="onCancel"
    />
  </form>

  <van-grid :column-num="2">
    <van-grid-item v-for="menuItem in foodsRef" :key="menuItem.id" icon="photo-o" :text="menuItem.name" />
  </van-grid>

</template>
