<template>
  <div class="app">
    <main>
      <OrderIcon />
      <!-- :search-keyword="searchKeyword"
        @input="updateSearchKeyword" -->
      <SearchInput v-model="searchKeyword" @search="searchProducts" />
      <ul>
        <li
          v-for="product in products"
          :key="product.id"
          class="item flex"
          @click="moveToDetailPage(product.id)"
        >
          <img
            class="product-image"
            :src="product.imageUrl"
            :alt="product.name"
          />
          <p>{{ product.name }}</p>
          <span>{{ product.price }}</span>
        </li>
      </ul>
      <div class="cart-wrapper">
        <button class="btn" @click="moveToCartPage">장바구니 바로가기</button>
      </div>
    </main>
  </div>
</template>

<script>
// import axios from 'axios'
// import ProductList from '~/components/ProductList.vue';
import OrderIcon from '~/components/OrderIcon.vue'
import SearchInput from '~/components/SearchInput.vue'
import { fetchProductByKeyword, fetchProducts } from '~/api'

export default {
  components: { OrderIcon, SearchInput },
  // 페이지 진입 전에 실행되므로 this 사용 불가
  async asyncData() {
    // 페이지 컴포넌트 아래서만 제공되는 속성.
    const res = await fetchProducts()
    // console.log(res)
    // const products = res.data.map(item => {
    //   return {
    //     ...item,
    //   imageUrl: `${item.imageUrl}?random=${Math.random()}`
    //   }
    // })
    const products = res.data.map((item) => ({
      ...item,
      imageUrl: `${item.imageUrl}?random=${Math.random()}`,
    }))
    return { products } // { products: products} 객체 축약 문법
  },
  data() {
    return {
      searchKeyword: '',
    }
  },

  methods: {
    moveToDetailPage(id) {
      // console.log(id)
      this.$router.push(`detail/${id}`)
    },
    async searchProducts() {
      const res = await fetchProductByKeyword(this.searchKeyword)
      // console.log(res.data)
      this.products = res.data.map((item) => ({
        ...item,
        imageUrl: `${item.imageUrl}?random=${Math.random()}`,
      }))
    },
    moveToCartPage() {
      this.$router.push('/cart')
    },
  },
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}
.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}
.product-image {
  width: 400px;
  height: 250px;
}
.app {
  position: relative;
}
.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}
.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>
