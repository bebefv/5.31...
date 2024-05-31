<template>
  <div class="product-list">
    <div v-for="product in products" :key="product.id" class="product-item">
      <img :src="product.image" alt="Product">
      <div class="product-info">
        <h3>{{ product.name }}</h3>
        <p>价格：{{ product.price }}</p>
        <button @click="addToCart(product)">添加到购物车</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: '商品1', price: 100, image: 'product1.jpg' },
        { id: 2, name: '商品2', price: 200, image: 'product2.jpg' },
        { id: 3, name: '商品3', price: 300, image: 'product3.jpg' }
      ]
    };
  },
  methods: {
    addToCart(product) {
      this.$emit('add-to-cart', product);
    }
  }
};
</script>

<style scoped></style>