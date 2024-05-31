<template>
  <div class="main-content">
    <!-- 全选复选框 -->
    <div class="check-all">
      <input type="checkbox" id="check-all">
      <label for="check-all">全选</label>
    </div>
    <!-- 新增商品表单 -->
    <form @submit.prevent="addProduct" class="add-product-form">
      <label for="product-name">商品名称:</label>
      <input type="text" id="product-name" v-model="productName" required>
      <label for="product-price">价格:</label>
      <input type="number" id="product-price" v-model.number="productPrice" required>
      <label for="product-quantity">数量:</label>
      <input type="number" id="product-quantity" v-model.number="productQuantity" required>
      <button type="submit">添加商品</button>
    </form>
    <!-- 商品列表 -->
    <div class="product-list">
      <ProductItem v-for="(product, index) in products" :key="index" :product="product"
        @remove-product="removeProduct(index)" />
    </div>
    <!-- 总金额 -->
    <div class="total-price">
      <span class="total-label">总金额：</span>
      <span class="total-amount">￥{{ totalPrice.toFixed(2) }}</span>
    </div>
    <!-- 结算按钮 -->
    <div class="checkout">
      <button class="btn-checkout" @click="checkout">去结算</button>
    </div>
  </div>
</template>

<script>
import ProductItem from './ProductItem.vue';

export default {
  components: {
    ProductItem,
  },
  data() {
    return {
      products: [],
      productName: '',
      productPrice: '',
      productQuantity: '',
    };
  },
  computed: {
    totalPrice() {
      return this.products.reduce((total, product) => total + (product.price * product.quantity), 0);
    },
  },
  methods: {
    addProduct() {
      const newProduct = {
        imgUrl: 'https://via.placeholder.com/150',
        name: this.productName,
        price: parseFloat(this.productPrice),
        quantity: parseInt(this.productQuantity),
      };
      this.products.push(newProduct);
      this.productName = '';
      this.productPrice = '';
      this.productQuantity = '';
    },
    removeProduct(index) {
      this.products.splice(index, 1);
    },
    checkout() {
      alert('总金额为：￥' + this.totalPrice.toFixed(2));
    },
  },
};
</script>

<style scoped>
.main-content {
  max-width: 1200px;
  margin: 20px auto;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.check-all {
  margin-bottom: 20px;
}

.check-all input[type="checkbox"] {
  margin-right: 5px;
}

.add-product-form {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.add-product-form label {
  flex: 1;
  margin-right: 10px;
}

.add-product-form input {
  flex: 2;
  margin-bottom: 10px;
  padding: 5px;
}

.add-product-form button {
  flex: 1;
  padding: 5px 10px;
  background-color: #ff6700;
  color: #fff;
  border: none;
  cursor: pointer;
}

.product-list {
  margin-bottom: 20px;
}

.total-price {
  margin-bottom: 20px;
  text-align: right;
}

.total-label {
  font-size: 18px;
}

.total-amount {
  font-size: 20px;
  color: #ff6700;
  font-weight: bold;
}

.checkout {
  text-align: right;
}

.btn-checkout {
  padding: 10px 20px;
  background-color: #ff6700;
  color: #fff;
  border: none;
  cursor: pointer;
}

/* ProductItem.vue样式 */
.product-item {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #e6e6e6;
  padding: 15px 0;
}

.product-item img {
  width: 80px;
  height: 80px;
  margin-right: 20px;
}

.product-info {
  flex: 1;
}

.product-info h3 {
  margin: 0 0 5px;
  font-size: 16px;
  color: #333;
}

.product-info p {
  margin: 0;
  font-size: 14px;
  color: #999;
}

.product-actions button {
  margin-left: 10px;
  padding: 5px 10px;
  background-color: #ff6700;
  color: #fff;
  border: none;
  cursor: pointer;
}
</style>