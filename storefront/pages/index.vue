// pages/index.vue
<template>
  <div>
    <h1>Welcome to the Medusa Nuxt Store</h1>
    <h2>Products</h2>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{ product.title }} - ${{ (product.variants[0].prices[0].amount / 100).toFixed(2)}}
      </li>
    </ul>
  </div>
</template>

<script setup>
const { data: { products } } = await useFetch('http://localhost:9000/store/products')
</script>