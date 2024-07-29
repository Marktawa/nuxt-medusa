<!-- pages/index.vue -->
<template>
  <div>
    <h1>Welcome to the Medusa Nuxt Store</h1>
    <h2>Products</h2>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{ product.title }} - ${{ (product.variants[0].prices[0].amount / 100).toFixed(2) }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'

const runtimeConfig = useRuntimeConfig()
const MEDUSA_URL = runtimeConfig.public.MEDUSA_URL
const { data } = await useFetch(`${MEDUSA_URL}/store/products`)
const products = data.value.products;

onMounted(async () => {
    await fetch(`${MEDUSA_URL}/store/carts`, {
        method: 'POST',
        credentials: "include",
    })
    .then((response) => response.json())
    .then(({ cart }) => {
        localStorage.setItem("cart_id", cart.id)
        console.log("The cart ID is " + localStorage.getItem("cart_id"));
    });
})  
  
</script>