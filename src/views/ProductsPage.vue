<template>
    <div id="app">
        <div class="carousel">
            <div v-for="(img, index) in images" :key="index" :class="{ active: index == currentIndex }">
                <img :src="img.src" />
            </div>
        </div>
    </div>
    <div class="text">Sản phẩm gợi ý</div>
    <div class="category">
    <span @click="setAll">Tất cả</span>
    <span @click="setGift">Set quà</span>
    <span @click="setBag">Túi</span>
    <span @click="setTeddy">Gấu bông</span>
    <span @click="setHeadphone">Tai nghe</span>
    </div>
    

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
            currentIndex: 0,
            value: '',
        };
    },
    methods: {
        setAll() {
            this.value = '';
            this.setproduct();
        },
        setGift() {
            this.value = 'set';
            this.setproduct();
        },
        setBag() {
            this.value = 'bag';
            this.setproduct();
        },
        setTeddy() {
            this.value = 'teddy';
            this.setproduct();
        },
        setHeadphone() {
            this.value = 'headphone';
            this.setproduct();
        },
        async setproduct(){
        const result = await axios.get(`/api/products`)
        const products = result.data;
        if (this.value == '') {
            this.products = products
        } else {
            this.products = products.filter(product => product.type == this.value);
        }
        }
    },
    async created() {
        const result = await axios.get(`/api/products`)
        const products = result.data;
        if (this.value == '') {
            this.products = products
        } else {
            this.products = products.filter(product => product.type == this.value);
        }
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
    margin-bottom: 20px;
}
.category{
    margin: auto;
    max-width: 900px;
}
span{
    background-color: antiquewhite;
    margin: 0 10px;
    border-radius: 100%;
    padding: 10px;
    color: purple;
    
}
span:hover{
    color: orangered;
    cursor: pointer;
    padding: 12px 10px;
}
</style>
