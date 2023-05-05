<template>
    <div v-if="product.type!=selectedValue" class="product-item">
        <router-link v-bind:to='"/products/" + product.id' >
            <div class="container-build"><img v-bind:src="product.imageUrl"></div>
        </router-link>
        <router-link v-bind:to='"/products/" + product.id' >
            <h3 class="product-name">{{ product.name }}</h3>
        </router-link>
        <h3 class="product-price">{{ product.price }}đ</h3>
        
        
    </div>
</template>

<script>

export default {
    name: 'ProductsGridItem',
    props:['product']
}
</script>

<style scoped>
.product-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 8px;
    box-shadow: 0px 2px 5px #888;
    display: flex;
    flex-direction: column;
    margin-bottom: 2%;

    position: relative;
    width: 23.5%;
    
}

.product-name {
    padding-top: 10px;
    font-size: 18px;
    margin: auto 15px;
}
.container-build{
    width: 100%;
    height: 200px;
    overflow: hidden;
    border-radius: 8px 8px 0px 0px;
}
img {
    height: 100%;
    width: 100%;
    transition: transform 0.2s ease-in-out;
}
img:hover{
    transform: scale(1.1); 
}

a {
    width: 100%;
    text-decoration: none;
    color: black;
   
}
a:hover{
    color: pink;
    text-decoration: none;
}
.product-price{
    margin-top: auto;
    
    padding: 20px 0;
    color: deeppink;
    font-size: 18px;
    font-weight: bold;
}
</style>