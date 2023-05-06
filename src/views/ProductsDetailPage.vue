<template>
  <div v-if="product">
    <div id="page-wrap">
      <div class="column-2">
        <div id="img-wrap">
          <img v-bind:src="product.imageUrl">
        </div>
        <div id="product-details">
          <h1>{{ product.name }}</h1>
          <div>
            <h3 id="price">{{ total }}.000đ</h3>
          </div>
          <div class="form-inline color">Mix:
            <button class="color1"></button>
            <button class="color2"></button>
            <button class="color3"></button>

          </div>
          <div class="form-inline border-side">
            <button class="button-mins" @click="decreaseQuantity">-</button>
            <span class="quantity">{{ quantity }}</span>
            <button class="button-add" @click="increaseQuantity">+</button>
          </div>
          <p>Đánh giá: {{ product.averageRating }}</p>
          <button id="add-to-cart" v-if="!itemIsInCart && !showSucessMessage" v-on:click="addToCart">Thêm vào giỏ</button>
          <button id="add-to-cart" class="green-button" v-if="!itemIsInCart && showSucessMessage">Sản phẩm đã thêm vào
            giỏ</button>
          <button id="add-to-cart" class="grey-button" v-if="itemIsInCart">Sản phẩm đã tồn tại trong giỏ hàng</button>

        </div>
      </div>
      <h4><br>Mô tả: </h4>
      <div class="border-describe">{{ product.description }}</div>
      <div class="text">Sản phẩm liên quan</div>
      <div id="page-wrap">
        <ProductsGrid :products="products" @click="loadProduct" />
      </div>
    </div>

  </div>
  <NotFoundPage v-else />
</template>

<script>
import axios from 'axios';
import NotFoundPage from './NotFoundPage.vue';
import ProductsGrid from '@/components/ProductsGrid.vue';
export default {
  name: "ProductsDetailPage",
  components: {
    NotFoundPage,
    ProductsGrid,
  },
  data() {
    return {
      product: {},
      cartItems: [],
      products: [],
      quantity: 1,
      showSucessMessage: false,
    };
  },
  computed: {
    itemIsInCart() {
      return this.cartItems.some(item => item.id === this.product.id);
    },
    total() {
      return this.quantity * this.product.price
    },
  },
  methods: {
    async addToCart() {
      await axios.post('/api/users/123/cart', {
        productId: this.$route.params.id,
      });
      this.showSucessMessage = true;
    },
    loadProduct() {
      window.location.reload()
    },
    increaseQuantity() {
      this.quantity++
    },
    decreaseQuantity() {
      if (this.quantity > 1) {
        this.quantity--
      }
    },
  },
  async created() {
    const { data: product } = await axios.get(`/api/products/${this.$route.params.id}`);
    this.product = product;
    const { data: cartItems } = await axios.get('/api/users/123/cart');
    this.cartItems = cartItems;

    const result = await axios.get(`/api/products`)
    const products = result.data;
    this.products = products.filter(product => product.type == this.product.type);
  }
};
</script>

<style scoped>
#page-wrap {
  margin-top: 16px;
  max-width: 900px;
}

.column-2 {
  display: flex;
  flex-direction: row;
}

#img-wrap {
  text-align: center;
}

img {
  width: 400px;
}

#product-details {
  padding: 10px 16px;
  position: relative;
}

#add-to-cart {
  width: 100%;
  align-items: center;
}

#price {
  top: 24px;
  right: 16px;
  color: deeppink;
  margin: 20px 0;
}

.green-button {
  background-color: green;
}

.grey-button {
  background-color: grey;
}

.border-describe {
  border: 1px solid black;
  padding: 10px;
}

.text {
  background-color: pink;
  color: deeppink;
  text-align: center;
  font-weight: bold;
  font-size: larger;
  padding: 8px;
  margin-top: 20px;
}

.border-side{
  border: 1px solid black;
  width: 35%;
  display: flex;
  justify-content: space-between;
  margin: 35px 0;
}
.button-mins{
  background-color: white;
  border-right: 1px solid black;
  color: black;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  text-align: center;
  justify-content: center;
  align-items: center;
  display: flex;
  justify-content: center;
}
.button-add{
  background-color: white;
  border-left: 1px solid black;
  color: black;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  text-align: center;
  justify-content: center;
  align-items: center;
  display: flex;
  justify-content: center;
}
.quantity{
  margin: 0 10px;
}

.color{
  margin: 30px 0;
}
.color1{
  border-radius: 50%;
  background-color: maroon;
  margin-left: 10px;
}
.color2{
  border-radius: 50%;
  background-color: blueviolet;
  margin-left: 10px;
}
.color3{
  border-radius: 50%;
  background-color: darkblue;
  margin-left: 10px;
}
</style>