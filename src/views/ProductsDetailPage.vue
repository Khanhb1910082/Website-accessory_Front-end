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
            <h3 id="price">{{ product.price }}đ</h3>
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
      showSucessMessage: false,
    };
  },
  computed: {
    itemIsInCart() {
      return this.cartItems.some(item => item.id === this.product.id);
    }
  },
  methods: {
    async addToCart() {
      await axios.post('/api/users/123/cart', {
        productId: this.$route.params.id,
      });
      this.showSucessMessage = true;
    },
    loadProduct(){
      window.location.reload()
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
</style>