<template>
  <div id="page-wrap">
    <h1>Giỏ hàng</h1>
    <ProductsList :products="cartItems" v-on:remove-from-cart="removeFromCart($event)" />
    <h3 id="total-price">Tổng: {{ totalPrice }}.000đ</h3>
    <button id="checkout-button">Thanh toán {{ itemCount }} sản phẩm</button>
  </div>
</template>

<script>
import axios from 'axios';
import ProductsList from '@/components/ProductsList.vue';
export default {
  name: 'CartPage',
  components: {
    ProductsList,
  },
  data() {
    return {
      cartItems: [],
      itemCount: 0,
    }
  },
  methods: {
    async removeFromCart(productId) {
      const result = await axios.delete(`/api/users/123/cart/${productId}`);
      this.cartItems = result.data;
      this.itemCount = this.itemCount-1;

    }
  },
  computed: {
    totalPrice() {
      return this.cartItems.reduce(
        (sum, item) => sum + Number(item.price), 0
      )
    }
  },
  async created() {
    const result = await axios.get('/api/users/123/cart');
    const cartItems = result.data;
    this.cartItems = cartItems;
  },
  mounted() {
    axios.get('/api/users/123/cart').then(response => {
      this.itemCount = response.data.length;
    })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style scoped>
h1 {
  border-bottom: 1px solid black;
  margin: 0;
  margin-top: 16px;
  padding: 16px;
}

#total-price {
  padding: 16px;
  text-align: right;
}

#checkout-button {
  width: 100%;
}
</style>