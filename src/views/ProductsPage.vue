<template>
    <div id="app">
        <div class="carousel">
            <div v-for="(img, index) in images" :key="index" :class="{ active: index == currentIndex }">
                <img :src="img.src" />
            </div>
        </div>
    </div>
    <div class="text">Sản phẩm gợi ý</div>
    <div id="page-wrap">
        <ProductsGrid :products="products" />
    </div>
</template>

<script>
import axios from 'axios';
import ProductsGrid from '@/components/ProductsGrid.vue';



export default {
    components: {
        ProductsGrid,
    },
    name: "ProductsPage",
    el: '#app',
    
    data() {
        return {
            products: [],
            images: [
                { src: '../images/slider0.png' },
                { src: '../images/slider1.png' },
                { src: '../images/slider2.png' },
            ],
            currentIndex: 0
        };
    },

    async created() {
        const result = await axios.get('/api/products')
        const products = result.data;
        this.products = products;
        setInterval(() => {
            this.currentIndex++;
            if (this.currentIndex >= this.images.length) {
                this.currentIndex = 0;
            }
        }, 7000);
    }
};
</script>
<style scoped>
.carousel {
    width: 100%;
    height: 500px;
    overflow: hidden;

}

.carousel>div {
    width: 100%;
    height: 100%;
    position: absolute;
    opacity: 0;
    transition: opacity .5s ease-in-out;
}

.carousel>div.active {
    opacity: 1;
}

img {
    width: 100%;
    max-height: 100%;
    display: block;
    margin: auto;
}

.text {
    background-color: pink;
    color: deeppink;
    text-align: center;
    font-weight: bold;
    font-size: larger;
    padding: 8px;
}
</style>
