<template>
    <div class="main-content">
        <input type="checkbox" v-model="checkAll" @change="toggleCheckAll" /> 全选
        <form @submit.prevent="addProduct">
            <label for="product-name">商品名称:</label>
            <input type="text" v-model="newProduct.name" required />
            <label for="product-price">价格:</label>
            <input type="number" v-model="newProduct.price" required />
            <label for="product-quantity">数量:</label>
            <input type="number" v-model="newProduct.quantity" required />
            <button type="submit">添加商品</button>
        </form>
        <div class="product-list">
            <ProductItem v-for="(product, index) in products" :key="index" :product="product"
                @update-quantity="updateQuantity" @remove-product="removeProduct" @checked="updateChecked" />
        </div>
        <div class="total-price">
            总金额：<span>￥{{ totalPrice.toFixed(2) }}</span>
        </div>
        <div class="checkout">
            <button @click="checkout">去结算</button>
        </div>
    </div>
</template>

<script>
import ProductItem from "./ProductItem.vue";

export default {
    name: "ShoppingCart",
    components: {
        ProductItem
    },
    data() {
        return {
            products: [
                {
                    imgUrl: "https://cbu01.alicdn.com/img/ibank/O1CN0159xqJy1RZkqWUnebJ_!!2214068622126-0-cib.jpg",
                    name: "维生素C软糖",
                    price: 18.8,
                    quantity: 1,
                    checked: false
                },
                {
                    imgUrl: "https://th.bing.com/th/id/R.3cca0dd6632c487fd0caf6c6aa11749a?rik=LQ65e%2bfJFZHURA&riu=http%3a%2f%2fwww.szquanli.com.cn%2fuploads%2fallimg%2f160906%2f2-160Z6103A7.jpg&ehk=OHHJm%2f4aCvERU%2bhXMyG%2bhIxX9DWv3OKLl6T8iNlKxQM%3d&risl=&pid=ImgRaw&r=0",
                    name: "汤臣倍健蛋白质乳粉",
                    price: 199.9,
                    quantity: 1,
                    checked: false
                },
                {
                    imgUrl: "https://cbu01.alicdn.com/img/ibank/O1CN01Gg2Qr51qv9pRyuy0D_!!3861015557-0-cib.jpg",
                    name: "森宝积木航空文创轰炸机战斗机",
                    price: 49.9,
                    quantity: 1,
                    checked: false
                },
                {
                    imgUrl: "https://th.bing.com/th/id/OIP.l9waHCSssiAOa7D-XH-IpwHaGv?rs=1&pid=ImgDetMain",
                    name: "钢铁侠抖音同款",
                    price: 24.8,
                    quantity: 1,
                    checked: false
                }
            ],
            checkAll: false,
            newProduct: {
                name: "",
                price: 0,
                quantity: 1
            }
        };
    },
    computed: {
        totalPrice() {
            return this.products.reduce((total, product) => {
                return total + (product.checked ? product.price * product.quantity : 0);
            }, 0);
        }
    },
    methods: {
        // 切换全选状态
        toggleCheckAll() {
            this.products.forEach(product => {
                product.checked = this.checkAll;
            });
        },
        // 更新商品数量
        updateQuantity(product, quantity) {
            product.quantity = quantity;
        },
        // 删除商品
        removeProduct(product) {
            this.products = this.products.filter(p => p !== product);
        },
        // 更新商品选中状态
        updateChecked(product, checked) {
            product.checked = checked;
        },
        // 添加新商品
        addProduct() {
            this.products.push({
                imgUrl: "https://via.placeholder.com/150",
                name: this.newProduct.name,
                price: this.newProduct.price,
                quantity: this.newProduct.quantity,
                checked: false
            });
            this.newProduct.name = "";
            this.newProduct.price = 0;
            this.newProduct.quantity = 1;
        },
        // 结算
        checkout() {
            alert("总金额为：￥" + this.totalPrice.toFixed(2));
        }
    }
};
</script>

<style scoped>
.main-content {
    max-width: 1200px;
    margin: 20px auto;
    padding: 20px;
    background-color: rgba(255, 255, 255, 0.8);
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

.product-list {
    margin-top: 20px;
}

.total-price {
    margin-top: 20px;
    text-align: right;
    color: #3ff5dd;
    font-weight: bold;
}

.checkout {
    margin-top: 20px;
    text-align: right;
}

.checkout button {
    padding: 10px 20px;
    background-color: #f46f36;
    color: #ffffff;
    border: none;
    cursor: pointer;
}
</style>