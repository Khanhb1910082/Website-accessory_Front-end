<template>
    <div class="row container-build">
        <div class="col-md-6 col-sm-6 col-xs-12 ">

            <div class="left">
                <ul>
                    <li><i class="fa fa-phone"></i> 0369818290 </li>
                    <li><i class="fa fa-envelope"></i> khanhb1305@gmail.com</li>
                </ul>
            </div>
        </div>

        <div class="col-md-6 col-sm-6 col-xs-12">
            <div class="right">
                <ul>
                    <li><i class="fa-brands fa-facebook"></i> facebook </li>
                    <li><i class="fa-brands fa-square-instagram"></i> instagram </li>
                    <li><i class="fa-brands fa-pinterest"></i> pinterest</li>
                </ul>
            </div>
        </div>
    </div>

    <div id="nav-bar">
        <router-link to="/products" id="products-link">
            <img style="display: inline;" src="../assets/logo.png" width="100">
            <h1 style="display: inline;">Turtle-K</h1>

        </router-link>
        <router-link to="/cart" id="cart-link">
            <button class="icon"> <i class="fa-solid fa-cart-shopping"><span class="badge">{{ itemCount
            }}</span></i></button>
        </router-link>
    </div>

    <nav class="navbar navbar-expand-lg background-pink">
        <a class="navbar-brand" href="#"></a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <router-link to="/products" class="nav-link">Tất cả </router-link>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Set quà </a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Gấu bông và gối </a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Balo và túi </a>
                </li>


            </ul>
            <form class="form-inline my-2 my-lg-0">
                <input class="form-control mr-sm-2" type="search" placeholder="Set quà tặng siêu hot" aria-label="Search">
                <button class="btn btn-danger my-2 my-sm-0" type="submit">Tìm kiếm</button>
            </form>
        </div>
    </nav>
</template>
<script>
import axios from 'axios';
export default {
    name: 'NavBar',
    data() {
        return {
            cartItems: [],
            itemCount: 0,
        }
    },

    mounted() {
        axios.get('/api/users/123/cart').then(response => {
            this.itemCount = response.data.length;
        })
            .catch(error => {
                console.log(error);
            });
    }
}
</script>
<style scoped>
.container-build {
    padding: 0 100px;
}

#nav-bar {
    line-height: 20px;
}

#products-link {
    justify-content: center;
    padding: 0 100px;
    display: inline-block;
    color: black;
    font-size: 22px;
    text-decoration: none;
}

#products-link h1 {
    padding-top: 15px;
    color: blueviolet;
}

#cart-link {
    position: absolute;
    right: 16px;
    top: 90px;
    right: 100px;
}

li:hover {
    color: firebrick;
}

ul li {
    margin-right: 10px;
    color: purple;
    list-style: none;
    display: inline-block;
}

a {
    color: purple;
}

a:hover {
    color: firebrick;
}

.right {
    text-align: end;
    margin-right: 20px;
}

.row {
    margin: auto;
    padding-top: 15px;
    background-color: pink;
}

.background-pink {
    background-color: pink;
    padding: 10px 100px;
}

button {
    border-radius: 30px;
}

.icon {
    position: relative;
    display: inline-block;
}

.badge {
    position: absolute;
    top: -10px;
    right: -10px;
    background-color: red;
    color: white;
    border-radius: 50%;
    padding: 5px 10px;
    font-size: 12px;
    line-height: 1;
}

.icon:before {
    content: "";
    position: absolute;
    z-index: -1;
    top: -5px;
    right: -5px;
    bottom: -5px;
    left: -5px;
}
</style>