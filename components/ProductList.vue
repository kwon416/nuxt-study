<template>
  <div>
    {{ products }}
  </div>
</template>

<script>
// import axios from 'axios'
import { fetchProducts } from '@/api'
export default {
  async asyncData() {
    // 페이지 컴포넌트 아래서만 제공되는 속성
    const res = await fetchProducts()
    // console.log(res)
    const products = res.data
    return { products } // { products: products} 객체 축약 문법
  },
}
</script>

<style></style>
