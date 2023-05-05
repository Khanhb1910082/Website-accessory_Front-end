<template>
    <div class="product-container">
        <img class="product-image" :src="product.imageUrl">
        <div class="details-wrap">
            <h3>{{ product.name }}</h3>
            <p>{{ product.price }}đ</p>

        </div>
        <button class="remove-button" v-on:click="$emit('remove-from-cart',product.id)"><i class="fa-solid fa-trash"></i></button>
    </div>
</template>

<script>
export default {
    name: 'ProductsListItem',
    props: ['product'],
}
</script>

<style scoped>
 .product-container {
    align-content: 'center';
    border-bottom: 1px solid #ddd;
    display: flex;
    padding: 16px;
    width: 100%;
  }

  .product-image {
    flex: 1;
    height: 100px;
    max-width: 100px;
  }

  .details-wrap {
    padding: 0 16px;
    flex: 3;
  }

  .remove-button {
    border-radius: 20px;
    padding: 10px 14px;
    margin: auto;
  }
</style>