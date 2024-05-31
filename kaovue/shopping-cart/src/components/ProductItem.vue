<template>
    <div class="product-item">
        <input type="checkbox" v-model="checked" @change="emitChecked" />
        <img :src="product.imgUrl" :alt="product.name" />
        <div class="product-info">
            <h3>{{ product.name }}</h3>
            <p>价格：<span class="price">￥{{ product.price }}</span></p>
            <p>数量：<span class="quantity">{{ product.quantity }}</span></p>
        </div>
        <div class="product-actions">
            <button @click="increaseQuantity">+</button>
            <button @click="decreaseQuantity">-</button>
            <button @click="removeProduct">删除</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ProductItem',
    props: {
        product: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            checked: false
        };
    },
    methods: {
        //增加商品数量
        increaseQuantity() {
            this.$emit('update-quantity', this.product, this.product.quantity + 1);
        },
        //减少商品数量
        decreaseQuantity() {
            if (this.product.quantity > 1) {
                this.$emit('update-quantity', this.product, this.product.quantity - 1);
            }
        },
        //删除商品
        removeProduct() {
            this.$emit('remove-product', this.product);
        },
        //发出商品选中状态变化的事件
        emitChecked() {
            this.$emit('checked', this.product, this.checked);
        }
    }
};
</script>

<style scoped>
.product-item {
    display: flex;
    align-items: center;
}

.product-item img {
    width: 130px;
    height: 100px;
    margin-right: 20px;
}

.product-info {
    flex-grow: 1;
}

.price-quantity {
    display: flex;
    justify-content: space-between;
}


.product-info h3 {
    margin: 0;
    font-size: 17px;
}

.product-info p {
    margin: 5px 0;
}

.product-actions button {
    margin-right: 10px;
    padding: 5px 10px;
    background-color: #f46b49;
    color: #ffffff;
    border: none;
    cursor: pointer;
}

.price {
    color: #f64d37;
    font-weight: bold;
}

.quantity {
    color: #5ea9f9;
    font-weight: bold;
}
</style>