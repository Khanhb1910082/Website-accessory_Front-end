<template>
    <div class="grid-wrap" >
        <ProductsGridItem v-for="product in products" :key="product.id" :product="product"/>
    </div>
</template>

<script>
import ProductsGridItem from './ProductsGridItem.vue';

export default {
    name: 'ProductsGrid',
     
    components: {
        ProductsGridItem,
    },
    props: ['products'],
}
</script>

<style scoped>
.grid-wrap {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-top: 16px;
}

</style>