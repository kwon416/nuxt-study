<template>
  <div>
    <div class="container">
      <div class="main-panel">
        <img
          class="product-image"
          :src="product.imageUrl"
          :alt="product.name"
        />
      </div>
      <div class="side-panel">
        <p class="name">{{ product.name }}</p>
        <p class="price">{{ product.price }}</p>
        <button type="button" @click="addToCart">카트에 담기</button>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from 'axios';
import { fetchProductById, createCartItem } from '@/api/index'

export default {
  async asyncData({ params }) {
    // console.log(params)
    const response = await fetchProductById(params.id)
    const product = response.data
    return { product }
  },
  head() {
    return {
      title: `Shopping Item Deatil - ${this.product.name}`,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `이 상품은 ${this.product.name}입니다.`,
        },
        {
          hid: 'og:title',
          name: 'og:title',
          content: `상품 상세 페이지`,
        },
        {
          hid: 'og:description',
          name: 'og:description',
          content: `상품 상세 정보`,
        },
        {
          hid: 'og:image',
          property: 'og:image',
          content: 'http://picsum.photos/640/480/',
        },
      ],
    }
  },
  methods: {
    async addToCart() {
      await createCartItem(this.product)
      this.$store.commit('addCartItem', this.product)
      this.$router.push('/cart')
    },
  },
  // created() {
  //     const id = console.log(this.$route.params.id)
  //     fetchProductById();
  // }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  margin: 2rem 0;
}
.product-image {
  width: 500px;
  height: 375px;
}
.side-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 220px;
  text-align: center;
  padding: 0 1rem;
}
</style>
